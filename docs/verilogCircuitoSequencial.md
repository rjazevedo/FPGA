# Circuito Sequencial

Até agora, todos os circuitos gerados foram circuitos combinacionais, que geram as saídas baseadas apenas nos valores das entradas e não guardam nenhuma informação internamente. A partir de agora, vamos olhar também para circuitos sequenciais, que são circuitos que guardam informações e as utilizam para gerar saídas futuras. Esses circuitos possuem sempre algum componente de memória internamente, que veremos em detalhes mais abaixo.

## Clock

Nesse material trabalharemos sempre com circuitos síncronos, isto é, circuitos que dependem de um clock para definir o momento exato onde as operações são efetivadas. O clock é um sinal de entrada do circuito e fornece uma frequência de operação para o mesmo.

Apesar de ser uma entrada, existem restrições para a frequência de clock que um circuito pode aceitar. Ao fazer todo o processo de modelagem de hardware e síntese de circuito, a ferramenta calcula a frequência máxima de operação que ele poderá ser executado. Então o clock só será efetivo se fornecer uma frequência até a frequência máxima de opração do circuito. A figura abaixo mostra a forma de onda típica do sinal de clock.

![Forma de onda do sinal de clock](img/onda.drawio.svg)

As duas setas da figura indicam momentos importantes do sinal de clock. Dizemos que o momento onde está a seta para cima é chamado de borda de subida e o momento da seta para baixo é chamado de borda de descida. Os circuitos que dependem de clock são construídos para armazenar dados numa das duas bordas do clock, sendo a borda de subida a mais comum delas. Existe uma tipo específico de circuito, os latches, que armazenam dados durante todo o intervalo onde o clock está com valor 1 ou com valor 0 mas não falaremos dos latches no momento.

Ao falar que o circuito armazena os dados na subida do clock, não estamos falando que todo o processamento deve acontecer somente nesse momento mas sim estamos falando que todos os dados processados durante o período inteiro serão armazenados durante a subida do clock.

## Reset

O sinal de reset é utilizado para retornar o circuito a um estado conhecido, também chamado de estado inicial. Existem circuitos que consideram o sinal de reset com valor 1 como ativo mas também existem circuitos que consideram o reset com valor 0 como ativo. Isso depende da implementação e a recomendação é manter um padrão pelo projeto inteiro. 

## Contador

O primeiro tipo comum de circuito sequencial que olharemos é o contador. Como o nome diz, um circuito contador é aquele que gera números sucessivos seguindo uma contagem. O código abaixo representa um contador em Verilog:

```verilog
module Contador(
    input wire clk,
    input wire reset,
    output reg [3:0] count
);

always @(posedge clk) begin
    if (reset)
        count <= 4'b0000;
    else
        count <= count + 1;
end

endmodule
```

O circuito acima representa um contador de 4 bits, que conta de forma crescente de 0 até 15, quando retorna ao valor zero (pois se somar 1 ao 15, considerando 4 bits, o próximo valor representado é 0). 

O sinal *count* do circuito está declarado como saída e como do tipo **reg**, o que significa que ele é um sinal de saída mas que o circuito também pode ler o valor que está nele (não como entrada no circuito mas sim como o valor que o próprio circuito escreveu nele). 

O bloco *always* tem agora um novo modificador quando declara o clock, que é o **posedge clk**, indicando que esse bloco é sensível à borda de subida do clock (ele poderia ser sensível à descida com **negedge clk**). Essa declaração indica que o block dentro do always só será executado na subida do clock.

Dentro do bloco, há um **if** para testar se o sinal de reset tem valor 1 (como reset é de um bit, esse if pode ser interpretado como *reset == 1*). Caso o reset esteja ativo, com valor 1, o contador terá atribuído o valor zero. Caso contrário, ele terá atribuído o próximo valor do contador. 

É possível mudar o contador para alterar o limite da contagem, como no código abaixo, que conta de 0 até 9, retornando ao 0.

```verilog
module Contador(
    input wire clk,
    input wire reset,
    output reg [3:0] count
);

always @(posedge clk) begin
    if (reset)
        count <= 4'b0000;
    else
        if (count == 10)
            count <= 4'b0000;
        else
            count <= count + 1;
end

endmodule
```

Também é possível desenvolver variações no valor inicial, começando de outros números, ao alterar a cláusula do reset e do reinício da contagem do código.

## Registrador de deslocamento

O registrador de deslocamento é um conjunto de registradores que desloca uma sequência de bits para um dos lados (direita ou esquerda). Existem múltiplas variações e veremos algumas abaixo. Começando com a versão básica abaixo:

```verilog
module Deslocamento(
    input wire clk,
    input wire reset,
    input wire shift_in,
    output reg [3:0] shift_out
);

reg [3:0] register;

always @(posedge clk) begin
    if (reset)
        register <= 4'b0000;
    else
        register <= {shift_in, register[3:1]};
end

assign shift_out = register;

endmodule
```

Você consegue ler e entender o código acima? Ele recebe um bit por vez através do sinal *shift_in* e gera uma saída através do sinal *shift_out* que contem sempre 4 bits, onde o sinal de entrada começa pela esquerda e vai avançando para a direita.

A linha 14 do código acima contem o operador {}, que concatena valores. No caso, ele concatena o bit de *shift_in* com os 3 bits mais significativos de *register*.

Esse deslocador é chamado de entrada serial e saída paralela pois entra com um bit e sai com 4 bits.

## Divisor de frequência

Um circuito muito comum é o divisor de frequência, que é um circuito que divide a frequência do clock por um valor fixo. O código abaixo mostra um divisor de frequência por 2:

```verilog
module Divisor(
    input wire clk,
    input wire reset,
    output reg clk_out
);

reg [1:0] count;

always @(posedge clk) begin
    if (reset)
        count <= 2'b00;
    else
        if (count == 2'b01)
            count <= 2'b00;
        else
            count <= count + 1;
end

assign clk_out = count[0];

endmodule
```

Esse circuito nada mais é que um contador que conta 2 valores (0 e 1) e gera o sinal de saída que é o bit menos significativo do contador. Como o contador conta de 0 até 1, o sinal de saída será 0 durante um ciclo de clock e 1 no próximo ciclo de clock, dividindo a frequência do clock por 2. Essa versão do código dá para ser simplificada removendo o bit mais significativo mas ela está assim para permitir fácil expansão para outros divisores que possam ser necessários. Os divisores que são potência de 2 são mais simples de fazer que os demais.

!!! Dica
    Esses componentes básicos são muito úteis e são a base para muitos outros circuitos sequenciais. Nem sempre eles aparecem de forma isolada como acima e você pode ve-los como parte de um circuito maior. Por exemplo, um contador pode ser usado para gerar endereços para uma memória e um registrador de deslocamento pode ser usado para fazer a leitura e escrita de dados em uma memória.

## Pratique

1. Faça um contador que conte de 3 até 11 e retorne ao 3
2. Faça um contador que conte para baixo, de 2 em 2, do 15 até o 1 e retorne ao 15
3. Faça o circuito de teste para os contadores acima e confirme a saída
4. Faça um registrador de deslocalmento que desloque para a esquerda
5. Faça um registrador de deslocamento que tenha a saída de apenas um bit
6. Faça circuitos de testes para os registradores acima
7. Faça um divisor de frequência por 4
8. Faça um divisor de frequência por 6
9. Faça circuitos de teste para os divisores acima



