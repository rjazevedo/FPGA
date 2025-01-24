# Portas Lógicas

## Introdução

Circuitos lógicos são a base da eletrônica digital. Eles são compostos por portas lógicas que realizam operações booleanas sobre sinais de entrada para produzir sinais de saída. Esses circuitos são fundamentais para o funcionamento de computadores, sistemas embarcados e diversos dispositivos eletrônicos. Nesse módulo, vamos explorar os conceitos básicos de circuitos lógicos para dar o embasamento aos componentes mais avançados que serão abordados nos módulos seguintes.

## Portas Lógicas

Sob a ótica desse curso, o menor componente que utilizaremos é uma porta lógica. Cada porta lógica realiza uma operação booleana específica sobre seus sinais de entrada para produzir um sinal de saída. 

Portas lógicas são os blocos básicos dos circuitos digitais. As principais portas lógicas são:

| Porta | Função | Descrição | Diagrama |
|-------|--------|-----------|--------|
| AND   | E      | Saída é 1 se todas as entradas são 1 | ![AND](img/and.png) |
| OR    | OU     | Saída é 1 se pelo menos uma entrada é 1 | ![OR](img/or.png) |
| NOT   | NÃO    | Inverte o sinal de entrada | ![NOT](img/not.png) |
| NAND  | NÃO E  | Saída é 0 se todas as entradas são 1 | ![NAND](img/nand.png) |
| NOR   | NÃO OU | Saída é 0 se pelo menos uma entrada é 1 | ![NOR](img/nor.png) |
| XOR   | OU Exclusivo | Saída é 1 se as entradas são diferentes | ![XOR](img/xor.png) |
| XNOR  | NÃO OU Exclusivo | Saída é 1 se as entradas são iguais | ![XNOR](img/xnor.png) |

Dos diagramas acima, pode-se ver que todas as portas lógicas possuem entradas (letras A e B do lado esquerdo da imagem) e uma saída (letra Q do lado direito da imagem). A saída é determinada pela operação lógica realizada pela porta. A junção de múltiplas portas lógicas forma o circuito digital desejado.
 
## Tabela Verdade

Uma tabela verdade é uma tabela que mostra todas as possíveis combinações de entradas e suas correspondentes saídas para uma operação lógica. 

### Porta AND

Aqui está a tabela verdade da porta AND com duas entradas que, relembrando da seção anterior, somente gera a saída 1 se todas as entradas forem 1:

| A | B | A AND B |
|---|---|---------|
| 0 | 0 |    0    |
| 0 | 1 |    0    |
| 1 | 0 |    0    |
| 1 | 1 |    1    |

### Porta OR

Aqui está a tabela verdade da porta OR com duas entradas que, relembrando da seção anterior, gera a saída 1 se pelo menos uma das entradas for 1:

| A | B | A OR B |
|---|---|--------|
| 0 | 0 |   0    |
| 0 | 1 |   1    |
| 1 | 0 |   1    |
| 1 | 1 |   1    |

### Porta NOT

Aqui está a tabela verdade da porta NOT que, relembrando da seção anterior, inverte o sinal de entrada:

| A | NOT A |
|---|-------|
| 0 |   1   |
| 1 |   0   |

### Porta NAND

Aqui está a tabela verdade da porta NAND com duas entradas que, relembrando da seção anterior, gera a saída 0 se todas as entradas forem 1:

| A | B | A NAND B |
|---|---|----------|
| 0 | 0 |    1     |
| 0 | 1 |    1     |
| 1 | 0 |    1     |
| 1 | 1 |    0     |

### Porta NOR

Aqui está a tabela verdade da porta NOR com duas entradas que, relembrando da seção anterior, gera a saída 0 se pelo menos uma das entradas for 1:

| A | B | A NOR B |
|---|---|---------|
| 0 | 0 |   1     |
| 0 | 1 |   0     |
| 1 | 0 |   0     |
| 1 | 1 |   0     |

### Porta XOR

Aqui está a tabela verdade da porta XOR com duas entradas que, relembrando da seção anterior, gera a saída 1 se as entradas forem diferentes:

| A | B | A XOR B |
|---|---|---------|
| 0 | 0 |   0     |
| 0 | 1 |   1     |
| 1 | 0 |   1     |
| 1 | 1 |   0     |

### Porta XNOR

Aqui está a tabela verdade da porta XNOR com duas entradas que, relembrando da seção anterior, gera a saída 1 se as entradas forem iguais:

| A | B | A XNOR B |
|---|---|----------|
| 0 | 0 |    1     |
| 0 | 1 |    0     |
| 1 | 0 |    0     |
| 1 | 1 |    1     |

## Expressões Lógicas

Expressões lógicas são combinações de portas lógicas que representam operações booleanas mais complexas. Elas são usadas para descrever o comportamento de circuitos digitais e podem ser simplificadas para reduzir o número de portas necessárias.

Existe todo um campo de estudo dedicado à simplificação de expressões lógicas, chamado de álgebra booleana, que não será tratado nesse curso pois pretendemos utilizar ferramentas para fazer a simplificação. Entretanto, é importante destacar que o número de portas lógicas influencia na complexidade do circuito e, justamente por isso, há um grande interesse em reduzir o número de portas necessárias.

### Exemplo

Vamos ver um exemplo de expressão lógica que utiliza portas lógicas para representar uma operação booleana. Considere a expressão:

```
F = A AND (B OR C)
```

Essa expressão lógica é composta por uma porta AND que recebe como entrada a variável A e o resultado de uma porta OR entre B e C. A tabela verdade dessa expressão seria:

| A | B | C | F |
|---|---|---|---|
| 0 | 0 | 0 | 0 |
| 0 | 0 | 1 | 0 |
| 0 | 1 | 0 | 0 |
| 0 | 1 | 1 | 0 |
| 1 | 0 | 0 | 0 |
| 1 | 0 | 1 | 1 |
| 1 | 1 | 0 | 1 |
| 1 | 1 | 1 | 1 |
