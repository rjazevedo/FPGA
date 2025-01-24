# Circuitos Sequenciais

## Introdução

Circuitos sequenciais são aqueles cujas saídas dependem tanto das entradas atuais quanto dos estados anteriores. Eles possuem memória e podem armazenar informações. Esses circuitos são fundamentais para a construção de sistemas digitais que requerem armazenamento e processamento de dados ao longo do tempo.

### Exemplo Motivador

Vamos considerar um exemplo motivador ao longo deste material: um contador de pessoas em uma sala. Esse contador deve ser capaz de registrar o número de pessoas que entram e saem da sala, armazenando o valor atual e atualizando-o conforme necessário.

## Flip-Flops

Flip-flops são os blocos básicos de memória em circuitos digitais. Eles podem armazenar um bit de informação e são usados para construir registradores e contadores. Existem vários tipos de flip-flops, cada um com características específicas: SR, D, JK e T. Nesse curso focaremos apenas nos flip-flops tipo D.

### Flip-Flop D

O Flip-Flop D possui uma entrada (D) e duas saídas (Q e Q'). A tabela verdade do Flip-Flop D é:

| D | Q | Q' |
|---|---|----|
| 0 | 0 |  1 |
| 1 | 1 |  0 |

O Flip-Flop D armazena o valor da entrada D na saída Q quando o sinal de clock é acionado. Ele é usado para armazenar um bit de informação em um circuito sequencial. Para armazenar múltiplos bits, vários flip-flops D podem ser utilizados.

## Contadores

Contadores são circuitos sequenciais que geram uma sequência de estados em resposta a pulsos de clock. Eles são usados para contar eventos, como o número de pessoas que entram em uma sala. Do módulo anterior, já foi apresentado o circuito do somador que era um circuito combinacional, capaz de gerar a saída logo após a atualização de uma das entradas. Nesse momento, estamos interessados num circuito sequencial, que só atualiza a saída após um pulso de clock.

### Contador Síncrono

Um contador síncrono é um tipo de contador onde todos os flip-flops são acionados simultaneamente pelo mesmo sinal de clock. Aqui está um exemplo de contador de 3 bits usando flip-flops.

| Estado | Q2 | Q1 | Q0 |
|--------|----|----|----|
|   0    |  0 |  0 |  0 |
|   1    |  0 |  0 |  1 |
|   2    |  0 |  1 |  0 |
|   3    |  0 |  1 |  1 |
|   4    |  1 |  0 |  0 |
|   5    |  1 |  0 |  1 |
|   6    |  1 |  1 |  0 |
|   7    |  1 |  1 |  1 |

## Registradores

Registradores são conjuntos de flip-flops usados para armazenar múltiplos bits de informação. Eles são usados para armazenar dados temporariamente durante o processamento.

### Registrador de Deslocamento

Um registrador de deslocamento é um tipo de registrador onde os dados podem ser deslocados para a esquerda ou para a direita. Aqui está um exemplo de registrador de deslocamento de 4 bits:

| Estado | Q3 | Q2 | Q1 | Q0 |
|--------|----|----|----|----|
|   0    |  0 |  0 |  0 |  0 |
|   1    |  0 |  0 |  0 |  1 |
|   2    |  0 |  0 |  1 |  0 |
|   3    |  0 |  1 |  0 |  0 |
|   4    |  1 |  0 |  0 |  0 |

## Conclusão

Circuitos sequenciais são essenciais para a construção de sistemas digitais que requerem armazenamento e processamento de dados ao longo do tempo. Flip-flops, contadores e registradores são componentes fundamentais desses circuitos. O exemplo motivador do contador de pessoas em uma sala ilustra como esses componentes podem ser usados para resolver problemas práticos.

