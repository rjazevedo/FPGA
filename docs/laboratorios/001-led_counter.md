# Contador de LEDs  

Na atividade anterior, construímos um simples **Blink**, que fazia um LED do kit FPGA piscar. Agora, vamos dar um passo adiante: nesta atividade, você trabalhará com **múltiplos LEDs**.  

## Recomendações  

Antes de iniciar, recomendamos que você leia o conteúdo disponível em [Circuito Sequencial](verilogCircuitoSequencial/), pois ele fornecerá a base necessária para esta atividade.  

## Atividade  

Seu objetivo é escrever um módulo Verilog chamado **LedCounter**, que deve:  

- Ter um **parâmetro** chamado `CLK_FREQ`, que representa a frequência do clock.  
- Ter como **entradas** os sinais `clk` (clock) e `rst_n` (reset ativo em nível baixo).  
- Ter como **saída** um sinal de 8 bits chamado `leds`.  

O comportamento esperado do módulo é simples: ele deve implementar um **contador de 8 bits**, exibindo seu valor nos LEDs. Esse contador deve:  

- **Incrementar a cada 1 segundo**, utilizando `CLK_FREQ` como referência.  
- **Iniciar com valor 0** quando `rst_n` estiver acionado.  

### Código inicial  

Como ponto de partida, você pode utilizar o esqueleto de código abaixo:  

```verilog
module LedCounter #(
    parameter CLK_FREQ = 25_000_000
) (
    input  wire clk,
    input  wire rst_n,
    output wire [7:0] leds
);

endmodule
```

## Entrega  

Para realizar a entrega, basta enviar o arquivo **led_counter.v** para o GitHub.  

O **GitHub Classroom** já está configurado para verificar a entrega e atribuir notas automaticamente com base nos testes.  

!!! note "Dica"
    Os testes do GitHub estão embutidos nos arquivos do laboratório. Se quiser saber mais sobre eles, consulte o script de correção `run sh` no repositório do GitHub. **Não altere os arquivos de correção!**   
