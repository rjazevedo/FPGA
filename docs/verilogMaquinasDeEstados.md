# Máquinas de Estados

## Visão Geral

Uma das categorias mais úteis de circuitos sequenciais são as máquinas de estados finitos, ou apenas **máquinas de estados**. Como estamos interessados em projetos maiores, vamos começar falando sobre elas aqui nesse tutorial. A figura abaixo contém uma ilustração da forma geral das máquinas de estados.

![Máquina de Estados](img/MaquinaEstados.drawio.svg)

Além das entradas (no canto esquerdo) e saídas (no canto direito), os demais componentes são:

* **Lógica de Entrada** recebe os sinais de entrada e também o estado atual e produz o novo estado da máquina de estado.
* **Lógica de Saída** recebe os sinais de entrada e o estado atual e produz os valores de saídas
* **Memória (estado)** guarda o estado atual do circuito

!!! Dica
    As máquinas de estados podem ser divididas em duas categorias, **Máquinas de Mealy** que são representadas exatamente como no diagrama acima e **Máquinas de Moore** que não permitem que os sinais de entrada sejam usados diretamente pela Lógica de Saída. Como regra geral, para evitar vários problemas de temporização, procure sempre utilizar Máquinas de Moore nos seu circuitos.

## Exemplo de Máquina de Estados

Vamos começar com um exemplo simples de uma máquina de estados que controla um semáforo de pedestres. O semáforo tem 3 estados: **verde**, **amarelo** e **vermelho**. A máquina de estados tem 2 entradas: **pedestre** e **tempo** e 3 saídas: **luzVerde**, **luzmArela** e **luzVermelha**. A figura abaixo mostra o diagrama de estados da máquina de estados.

![Diagrama de Estados do Semáforo](img/semaforo.drawio.svg)

Um diagrama de estados indica os estados possíveis do circuito e as transições entre eles. Cada estado é representado por um círculo e as transições são representadas por setas. Cada transição é rotulada com a condição que faz a transição acontecer. No caso do semáforo, a condição é o tempo que passou desde a última transição e o botão que o pedestre aperta para atravessar. O diagrama também indica, através de uma seta, qual é o estado inicial do circuito, no caso, o verde.

O circuito abaixo implementa a máquina de estados do semáforo:

```verilog
module Semaforo(
    input wire clk,
    input wire reset,
    input wire pedestre,
    output reg luzVerde,
    output reg luzAmarela,
    output reg luzVermelha
);

reg [1:0] estado;
reg [4:0] tempo;
reg zeraTempo;

always @(posedge clk) begin
    if (zeraTempo)
        tempo = 0;
    else
        tempo = tempo + 1;
end


always @(posedge clk) begin
  if (reset == 1) begin
    estado = 2'b00;
    zeraTempo = 1;
  end
  else begin
    zeraTempo = 0;
    case (estado)
      2'b00: begin
        if (tempo == 5'd20) begin
          estado = 2'b01;
          zeraTempo = 1;
        end
        else if (pedestre) begin
          estado = 2'b01;
          zeraTempo = 1;
        end
      end
      2'b01: begin
        if (tempo == 5'd10) begin
          estado = 2'b10;
          zeraTempo = 1;
        end
      end
      2'b10: begin
        if (tempo == 5'd30) begin
          estado = 2'b00;
          zeraTempo = 1;
        end
      end
      default: begin
        estado = 2'b00;
        zeraTempo = 1;
      end
    endcase
  end
end

always @(estado) begin
  case (estado)
    2'b00: begin
      luzVerde <= 1;
      luzAmarela <= 0;
      luzVermelha <= 0;
    end
    2'b01: begin
      luzVerde <= 0;
      luzAmarela <= 1;
      luzVermelha <= 0;
    end
    2'b10: begin
      luzVerde <= 0;
      luzAmarela <= 0;
      luzVermelha <= 1;
    end
    default: begin
      luzVerde <= 0;
      luzAmarela <= 0;
      luzVermelha <= 0;
    end
  endcase
end

endmodule

```

O código acima implementa um contador chamado *tempo*, bem similar ao que vimos anteriormente. Ele é incrementado a cada ciclo de clock e tem como reset o sinal *zeraTempo*. O estado do semáforo é guardado no registrador *estado* e é atualizado a cada ciclo de clock. A lógica de saída é implementada através de um *case* que verifica o estado atual e decide o que fazer dadas as entradas. O código checa pela variável *tempo* para realizar as transições entre os estados (de verde para amarelo, de amarelo para vermelho e de vermelho para verde). A transição entre verde e amarelo também é feita através do sinal *pedestre*. Não estamos tratando de informações sobre a frequência do *clock*, apenas que o número de ciclos da variável tempo foi configurado para simular o tempo de um semáforo.

Logo a seguir existe um outro bloco *always* que cuida apenas de gerar a saída baseada no estado atual. Não é incomum encontrar esse código mesclado com o *aways* anterior mas preferimos deixa-lo separado por questões de legibilidade. Note que os dois cases possuem a cláusula *default* que é executada quando o estado não é nenhum dos outros. Isso é uma boa prática para garantir que todas as saídas são definidas em todos os estados.

!!! Dica
    O código acima é um exemplo de uma máquina de estados finitos. Ele é um exemplo de uma máquina de Moore, pois as saídas são determinadas apenas pelo estado atual. O código também é um exemplo de uma máquina de estados com saídas codificadas, pois as saídas são determinadas diretamente pelo estado atual, sem lógica adicional.

!!! Atenção
    Notou que utilizamos dois sinais para atribuição (= e <=)? Existem dois tipos de atribuições em Verilog, as bloqueantes (=) e as não bloqueantes (<=). A atribuição bloqueante é utilizada para atribuir valores a variáveis em sequência, ou seja, a próxima atribuição só ocorre após a primeira ter sido realizada. A atribuição não bloqueante é utilizada para atribuir valores a variáveis em paralelo, ou seja, todas as atribuições ocorrem ao mesmo tempo. No caso do código acima, a atribuição bloqueante é utilizada para o contador de tempo e a atribuição não bloqueante é utilizada para as saídas. Falaremos mais sobre isso em um tutorial futuro. Por enquanto, procure utilizar as bloqueantes (=) dentro de máquinas de always que são sensíveis a mudança de clock pois essa é a semântica que você está acostumado a entender em outras linguagens (se o código fosse em C, o comportamento seria similar à sua interpretação do código acima com =).

## Pratique

1. Agora que você já viu um exemplo de máquina de estados, tente implementar uma máquina de estados que controla um semáforo de carros. O semáforo de carros tem 3 estados: **verde**, **amarelo** e **vermelho**. A máquina de estados tem 1 entrada: **tempo** e 3 saídas: **luzVerde**, **luzmArela** e **luzVermelha**. O diagrama de estados é o mesmo do semáforo de pedestres, mas as transições são todas baseadas em tempo. 
2. Faça o módulo de teste para testar o circuito acima.
3. Lembra do circuito de alerta do carro? Faça um módulo que receba cada sinal de alerta e controle uma luz para piscar enquanto o alerta estiver ativo.

