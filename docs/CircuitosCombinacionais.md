# Circuitos Combinacionais

## Introdução

Circuitos combinacionais são aqueles cujas saídas dependem apenas das entradas atuais. Eles não possuem memória e não armazenam estados anteriores. Esses circuitos são fundamentais para a construção de sistemas digitais, pois realizam operações lógicas e aritméticas básicas.

## Exemplos de Circuitos Combinacionais

### Somadores

Somadores são circuitos combinacionais que realizam operações de adição. Existem dois tipos principais de somadores:

- **Meio Somador (Half Adder)**: Realiza a adição de dois bits.
- **Somador Completo (Full Adder)**: Realiza a adição de três bits (dois bits de entrada e um bit de vai um).

#### Meio somador

O meio somador possui duas entradas (A e B) e duas saídas (Soma e Vai um). A tabela verdade do somador meio é:

| A | B | Soma | Vai um |
|---|---|------|------------|
| 0 | 0 |  0   |     0      |
| 0 | 1 |  1   |     0      |
| 1 | 0 |  1   |     0      |
| 1 | 1 |  0   |     1      |

#### Somador Completo

O somador completo possui três entradas (A, B e Vai um de Entrada) e duas saídas (Soma e Vai um de Saída). A tabela verdade do somador completo é:

| A | B | Vai um de Entrada | Soma | Vai um de Saída |
|---|---|-----------------------|------|---------------------|
| 0 | 0 |          0            |  0   |         0           |
| 0 | 0 |          1            |  1   |         0           |
| 0 | 1 |          0            |  1   |         0           |
| 0 | 1 |          1            |  0   |         1           |
| 1 | 0 |          0            |  1   |         0           |
| 1 | 0 |          1            |  0   |         1           |
| 1 | 1 |          0            |  0   |         1           |
| 1 | 1 |          1            |  1   |         1           |

### Multiplexadores

Multiplexadores são circuitos combinacionais que selecionam uma de várias entradas e a encaminham para a saída. Eles são usados para direcionar dados de diferentes fontes para um único destino. As vezes são chamados também de **Seletor**.

#### Multiplexador 2:1

Um multiplexador 2:1 possui duas entradas de dados (D0 e D1), uma entrada de seleção (S) e uma saída (Y). A tabela verdade do multiplexador 2:1 é:

| S | Y |
|---|---|
| 0 | D0|
| 1 | D1|

Note que o valor que estiver na entrada D0, independente de ser 0 ou 1, será encaminhado para a saída Y quando a entrada de seleção S for 0. E o valor que estiver na entrada D1 será encaminhado para a saída Y quando a entrada de seleção S for 1.

#### Multiplexador 4:1

Um multiplexador 4:1 possui quatro entradas de dados (D0, D1, D2, D3), duas entradas de seleção (S0 e S1) e uma saída (Y). A tabela verdade do multiplexador 4:1 é:

| S1 | S0 | Y |
|----|----|---|
|  0 |  0 | D0|
|  0 |  1 | D1|
|  1 |  0 | D2|
|  1 |  1 | D3|

### Decodificadores

Decodificadores são circuitos combinacionais que convertem um código binário de entrada em um único sinal de saída. Eles são usados para selecionar uma linha específica em um conjunto de linhas.

#### Decodificador 2:4

Um decodificador 2:4 possui duas entradas (A e B) e quatro saídas (Y0, Y1, Y2, Y3). A tabela verdade do decodificador 2:4 é:

| A | B | Y0 | Y1 | Y2 | Y3 |
|---|---|----|----|----|----|
| 0 | 0 |  1 |  0 |  0 |  0 |
| 0 | 1 |  0 |  1 |  0 |  0 |
| 1 | 0 |  0 |  0 |  1 |  0 |
| 1 | 1 |  0 |  0 |  0 |  1 |

## Simplificação de Circuitos Combinacionais

A simplificação de circuitos combinacionais é importante para reduzir o número de portas lógicas necessárias, o que pode economizar espaço e energia. A álgebra booleana e os mapas de Karnaugh são ferramentas comuns usadas para simplificar expressões lógicas. Nesse curso, contaremos com ferramentas para fazer a simplificação das expressões lógicas.

### Álgebra Booleana

A álgebra booleana utiliza leis e teoremas para simplificar expressões lógicas. Algumas das leis mais importantes são:

- Lei de De Morgan
- Lei da Identidade
- Lei da Anulação
- Lei da Idempotência

### Mapas de Karnaugh

Os mapas de Karnaugh são uma ferramenta gráfica usada para simplificar expressões lógicas. Eles organizam as combinações de entradas em uma tabela de forma que os termos adjacentes possam ser facilmente identificados e combinados.

## Conclusão

Circuitos combinacionais são essenciais para a construção de sistemas digitais. Eles realizam operações lógicas e aritméticas básicas e podem ser combinados para formar circuitos mais complexos. A simplificação de circuitos combinacionais é importante para otimizar o uso de recursos e melhorar a eficiência dos sistemas digitais.
