# Botão  

Até agora, nossos circuitos tiveram apenas **saídas**, com as únicas entradas sendo sinais de controle, como o **clock (`clk`)** e o **reset (`rst_n`)**. Nesta atividade, introduziremos o uso de **entradas externas**, utilizando um **botão** como exemplo.  

## Debouncing  

Ao utilizar **interruptores físicos**, como botões e switches, o contato **não ocorre de forma instantânea**. Durante o processo de acionamento, pode ocorrer um efeito indesejado chamado **bouncing**, que consiste em **oscilações** no estado do botão antes que ele estabilize.  

Para corrigir esse problema, existem várias abordagens, como:  

- Utilização de um **registrador** para armazenar o estado do botão.  
- Uso de um **latch** [(saiba mais)](https://embarcados.com.br/latch/).  
- Implementação de um **contador** que considera o botão pressionado apenas após um certo tempo.  

Nesta atividade, você pode utilizar uma **abordagem mais simples**, implementando um **único registrador de 1 bit** como debounce. Esse registrador armazenará o valor do botão **a cada ciclo de clock**, ajudando a suavizar os efeitos do bouncing.  

Para uma explicação mais detalhada sobre **debouncing**, recomendamos a leitura deste [artigo](https://circuitdigest.com/electronic-circuits/what-is-switch-bouncing-and-how-to-prevent-it-using-debounce-circuit).  

## Atividade  

Seu objetivo é escrever um módulo Verilog chamado **Button**, que deve:  

- Ter como **entradas** os sinais:  
  - `clk` (clock).  
  - `rst_n` (reset ativo em nível baixo).  
  - `btn` (botão, ativo em nível alto).  
- Ter como **saída** um sinal de 1 bit chamado `led`.  

### Comportamento esperado  

- Sempre que o botão for **pressionado**, o **LED deve acender**.  
- Se o botão permanecer **pressionado**, o **LED deve continuar aceso**.  
- Quando o botão for **solto**, o **LED deve apagar**.  
- Ao **resetar o circuito**, o **LED deve ficar apagado**.  

### Código inicial  

Como ponto de partida, você pode utilizar o esqueleto de código abaixo:  

```verilog
module Button (
    input  wire clk,
    input  wire rst_n,
    input  wire btn,
    output wire led
);

endmodule
```

## Entrega  

Para realizar a entrega, basta enviar o arquivo **button.v** para o GitHub.  

O **GitHub Classroom** já está configurado para verificar a entrega e atribuir notas automaticamente com base nos testes.  

!!! note "Dica"
    Os testes do GitHub estão embutidos nos arquivos do laboratório. Se quiser saber mais sobre eles, consulte o script de correção `run sh` no repositório do GitHub. **Não altere os arquivos de correção!**  