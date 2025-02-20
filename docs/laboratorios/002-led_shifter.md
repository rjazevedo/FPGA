# Deslocamento de LEDs  

Até o momento, construímos apenas circuitos que utilizam somadores. Nesta atividade, exploraremos a **operação de deslocamento (shift)**.  

## Recomendações  

Antes de iniciar, recomendamos que você leia o conteúdo disponível em [Circuito Sequencial](verilogCircuitoSequencial/), pois ele fornecerá a base necessária para esta atividade.  

## Deslocamento Circular  

Nesta atividade, utilizaremos o conceito de **deslocamento circular**, no qual:  

- O **bit mais significativo** de um registrador se torna o **menos significativo**.  
- O **menos significativo** passa a ocupar a posição do **segundo menos significativo**, e assim por diante.  

A imagem abaixo ilustra essa operação:  

![Circular shift](/img/circular_shifft.png)  

## Atividade  

Seu objetivo é escrever um módulo Verilog chamado **LedShifter**, que deve:  

- Ter um **parâmetro** chamado `CLK_FREQ`, que representa a frequência do clock.  
- Ter como **entradas** os sinais `clk` (clock) e `rst_n` (reset ativo em nível baixo).  
- Ter como **saída** um sinal de 8 bits chamado `leds`.  

O comportamento esperado do módulo é semelhante ao da atividade anterior, com a diferença de que, em vez de incrementar um contador, será realizado um **deslocamento circular para a esquerda** em um registrador de 8 bits.  

- **Executar um deslocamento a cada 1 segundo**, utilizando `CLK_FREQ` como referência.  
- **Iniciar com o valor 5 (`8'b00011111`)** quando `rst_n` estiver acionado.  

### Código inicial  

Como ponto de partida, você pode utilizar o esqueleto de código abaixo:  

```verilog
module LedShifter #(
    parameter CLK_FREQ = 25_000_000
) (
    input  wire clk,
    input  wire rst_n,
    output wire [7:0] leds
);

endmodule
```

## Entrega  

Para realizar a entrega, basta enviar o arquivo **led_shifter.v** para o GitHub.  

O **GitHub Classroom** já está configurado para verificar a entrega e atribuir notas automaticamente com base nos testes.  

!!! note "Dica"
    Os testes do GitHub estão embutidos nos arquivos do laboratório. Se quiser saber mais sobre eles, consulte o script de correção `run sh` no repositório do GitHub. **Não altere os arquivos de correção!**  
