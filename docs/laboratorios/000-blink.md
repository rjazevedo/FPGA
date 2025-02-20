# Começando do início  

Sempre que aprendemos uma nova linguagem de programação, escrevemos um "Hello World" para testar a linguagem e nos dar boa sorte. No mundo do hardware, esse "Hello World" geralmente se transforma em um "Blink", que consiste basicamente em fazer um LED piscar. Para manter a tradição, também iniciaremos com um Blink, utilizando ferramentas de simulação e o kit FPGA.  

## Instalando o ferramental  

Para realizar a instalação das ferramentas necessárias, recomendo seguir o guia disponível em: [Instalação](/guias/instalacao).  

## Construindo o Blink  

Esta atividade é baseada nas [noções básicas de Verilog](/verilogNocoesBasicas/) apresentadas na bibliografia do curso. Se ainda não leu esse material, recomendo fortemente que o faça antes de prosseguir.  

O Blink consiste, essencialmente, em fazer um LED piscar. Para isso, precisamos definir uma frequência de oscilação, o que requer um sinal de clock de referência. Neste circuito, utilizaremos um clock de 25 MHz fornecido por um pino da FPGA. Dessa forma, nosso circuito terá como entrada um sinal de clock e um sinal de reset (ativo em nível baixo) e, como saída, um LED.  

Internamente, usaremos um registrador de 32 bits para contar os ciclos de clock e determinar o momento de alternar o estado do LED. O circuito consiste basicamente em um somador que incrementa esse registrador a cada ciclo de clock. Quando ele atinge um valor predeterminado, o estado do LED é invertido.  

Por exemplo, para fazer o LED piscar uma vez a cada meio segundo com um clock de 25 MHz, precisamos contar até **12_500_000** ciclos. (Observe que utilizei **'_'** para separar as ordens de grandeza, em vez de **'.'**, pois essa notação pode ser usada em Verilog para representar números inteiros em diferentes bases, como decimal, binário, hexadecimal ou octal). Como nosso clock tem **25_000_000** ciclos por segundo contaremos até **12_500_000**, quando o contador atingir esse valor, inverteremos o estado do LED e reiniciaremos a contagem, desta forma inverteremos o estado do led a cada meio segundo.  

O código Verilog abaixo implementa esse circuito:  

```verilog
module Blink #(
    parameter CLK_FREQ = 25_000_000 
) (
    input wire clk,
    input wire rst_n,
    output reg led
);

localparam ONE_SECOND  = CLK_FREQ;
localparam HALF_SECOND = CLK_FREQ / 2;

reg [32:0] counter;

always @(posedge clk ) begin
    if (!rst_n) begin
        counter <= 32'h0;
        led     <= 1'b0;
    end else begin
        if (counter >= HALF_SECOND) begin
            counter <= 1'b0;
            led     <= ~led;
        end else begin
            counter <= counter + 1'b1;
        end
    end
end
    
endmodule
```

Se desejar alterar a velocidade do piscar do LED, basta modificar o valor máximo do contador. No exemplo acima, ele conta até **HALF_SECOND - 1**.  

## Rodando no FPGA  

Para testar o exemplo na FPGA, precisamos conectar as entradas e saídas do nosso design aos pinos físicos da FPGA. Para isso, utilizamos um arquivo **LPF**, onde associamos nomes a pinos físicos e definimos suas características. O exemplo abaixo mostra como essa associação é feita:  

```plaintext
LOCATE COMP "reset" SITE "H4";
IOBUF  PORT "reset" IO_TYPE=LVCMOS33;

LOCATE COMP "led" SITE "N4";
IOBUF  PORT "led" IO_TYPE=LVCMOS33;

LOCATE COMP "clk" SITE "P3";
IOBUF  PORT "clk" IO_TYPE=LVCMOS33;
FREQUENCY PORT "clk" 25.0 MHz;
```

No exemplo acima:  

- O nome de cada pino é atribuído pela diretiva `LOCATE COMP "nome" SITE "pino físico";`  
- O tipo do pino é definido com `IOBUF PORT "nome" IO_TYPE=LVCMOS33;`  
- Para pinos de clock, a frequência é especificada com `FREQUENCY PORT "nome" 25.0 MHz;`  

### Carregando no FPGA  

Para carregar o Blink na FPGA, salve o código Verilog em um arquivo **blink.v** e o mapeamento de pinos em um arquivo **pinout.lpf**.  

Com o kit FPGA conectado ao computador, execute os seguintes comandos:  

```bash
yosys -p "read_verilog blink.v; synth_ecp5 -json out.json -top Blink"
nextpnr-ecp5 --json out.json --lpf pinout.lpf --textcfg out.config \
    --package CABGA381 --45k --speed 6
ecppack --input out.config --bit out.bit
openFPGALoader -b colorlight-i9 out.bit
```

Se tudo ocorreu corretamente, um LED na sua FPGA deve estar piscando.  

### Explicação dos comandos  

1. **yosys**: Ferramenta de síntese. Converte o código Verilog de alto nível em uma **netlist** de baixo nível. No comando, pedimos ao Yosys para:  
   - Ler o arquivo `blink.v`  
   - Sintetizar o design para a arquitetura **ECP5**  
   - Gerar a saída em `out.json`  
   - Definir `Blink` como o módulo principal (`-top Blink`)  

2. **nextpnr-ecp5**: Ferramenta de **Placement and Route (PnR)**. Posiciona os elementos do circuito dentro da FPGA e realiza o roteamento das conexões. No comando, fornecemos:  
   - A netlist gerada pelo Yosys (`out.json`)  
   - O mapeamento de pinos (`pinout.lpf`)  
   - A saída (`out.config`)  
   - O modelo do FPGA (`CABGA381`), a variante **45K** e o speed grade **6**  

3. **ecppack**: Gera o **bitstream** final (`out.bit`), que contém a configuração a ser carregada na FPGA.  

4. **openFPGALoader**: Carrega o bitstream na FPGA.  

## Simulando  

Antes de carregar um design em uma FPGA, uma boa prática é simulá-lo para evitar problemas difíceis de depurar.  

Para isso, utilizaremos o **Icarus Verilog (iverilog)**, que requer um **testbench**. O código abaixo implementa um testbench básico para o Blink:  

```verilog
`timescale 1ns/1ns
module blink_tb();

reg clk, rst_n;
wire led;

initial begin
    $dumpfile("blink.vcd");
    $dumpvars;
    clk = 0;
    rst_n = 0;
    
    #2 rst_n = 1;
    #1000 $finish;
end

Blink #(
    .CLK_FREQ(50)
) U1(
    .clk   (clk),
    .rst_n (rst_n),
    .led   (led)
);

always #1 clk = ~clk;

endmodule
```

Esse testbench gera um arquivo **blink.vcd**, contendo a evolução dos sinais ao longo do tempo. Esse arquivo pode ser visualizado com ferramentas como **GTKWave** ou a extensão **WaveTrace** no VSCode.  

O passo a passo detalhado de como rodar a simulação e visualizar o resultado está disponível em: [Como Simular](/verilogComoSimular/).  

## Entrega  

O objetivo desta atividade é familiarizar-se com o ambiente de desenvolvimento. Como primeira entrega, basta enviar o arquivo **blink.v** para o GitHub.  

O **GitHub Classroom** já está configurado para verificar a entrega e atribuir notas automaticamente com base nos testes.  

Para as próximas atividades, forneceremos apenas a especificação do módulo principal (top module), incluindo entradas, saídas e nomes de sinais.  

**Dica**: Os testes do GitHub estão embutidos nos arquivos do laboratório. Se quiser saber mais sobre eles, veja o script de correção `run.sh` no repositório do GitHub. **Não altere os arquivos de correção!**  
