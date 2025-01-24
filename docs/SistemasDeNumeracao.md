# Sistemas de Numeração

## Introdução

Os sistemas de numeração são formas de representar números usando símbolos. Os sistemas de numeração mais comuns são o decimal (base 10), binário (base 2), octal (base 8) e hexadecimal (base 16). Cada sistema de numeração tem sua própria base e conjunto de símbolos. Neste material, vamos focar no sistema binário, que é fundamental para a eletrônica digital e a computação.

## Sistema Decimal

O sistema decimal é o sistema de numeração mais comum e utiliza a base 10. Ele usa os dígitos de 0 a 9 para representar números. Cada posição em um número decimal tem um valor posicional que é uma potência de 10.

### Exemplo

O número 345 no sistema decimal pode ser representado como:

```
345 = 3 * 10^2 + 4 * 10^1 + 5 * 10^0
345 = 3 * 100 + 4 * 10 + 5 * 1
```

Note que o valor posicional está indicando a quantidade de vezes que o dígito é multiplicado pela base elevada à posição. Assim, o 4, segundo dígito da direita para a esquerda, está multiplicado por 10 elevado à primeira potência, o que significa que ele tem o valor 40 na representação decimal.

## Sistema Binário

O sistema binário utiliza a base 2 e usa apenas os dígitos 0 e 1 para representar números. Cada posição em um número binário tem um valor posicional que é uma potência de 2. A metodologia é a mesma do decimal mas agora com apenas dois valores para representarem os dígitos.

### Exemplo

O número 1011 no sistema binário pode ser representado como:

```
1011 = 1 * 2^3 + 0 * 2^2 + 1 * 2^1 + 1 * 2^0
     = 8 + 0 + 2 + 1
     = 11 (decimal)
```

## Conversão de Bases

### Decimal para Binário

Para converter um número decimal para binário, podemos usar o método da divisão sucessiva por 2.

#### Exemplo

Vamos converter o número decimal 13 para binário:

```
13 / 2 = 6, resto 1
 6 / 2 = 3, resto 0
 3 / 2 = 1, resto 1
 1 / 2 = 0, resto 1
```

Lendo os restos de baixo para cima, obtemos o número binário 1101.

### Binário para Decimal

Para converter um número binário para decimal, multiplicamos cada dígito binário pela potência de 2 correspondente e somamos os resultados.

#### Exemplo

Vamos converter o número binário 1101 para decimal:

```
1101 = 1 * 2^3 + 1 * 2^2 + 0 * 2^1 + 1 * 2^0
     = 8 + 4 + 0 + 1
     = 13 (decimal)
```

## Representação Posicional

A representação posicional dos números é uma forma de expressar números em diferentes bases, onde o valor de cada dígito depende da sua posição e da base do sistema de numeração.

### Exemplo

No sistema binário, o número 1011 tem a seguinte representação posicional:

```
1 * 2^3 + 0 * 2^2 + 1 * 2^1 + 1 * 2^0
```

## Deslocamentos

Os deslocamentos são operações que movem os bits de um número binário para a esquerda ou para a direita. Eles são usados para multiplicar ou dividir números por potências de 2.

### Deslocamento para a Esquerda

O deslocamento para a esquerda (<<) multiplica o número por 2.

#### Exemplo

```
1011 << 1 = 10110 (multiplicação por 2)
```

### Deslocamento para a Direita

O deslocamento para a direita (>>) divide o número por 2.

#### Exemplo

```
1011 >> 1 = 101 (divisão por 2)
```

## Números Sinalizados em Complemento de 2

A representação de números sinalizados em complemento de 2 é uma forma de representar números negativos em binário. O bit mais significativo (MSB) é usado como bit de sinal, onde 0 indica um número positivo e 1 indica um número negativo.

### Exemplo

Vamos representar o número -5 em complemento de 2 usando 4 bits:

1. Representar o número 5 em binário: 0101
2. Inverter os bits: 1010
3. Adicionar 1: 1010 + 1 = 1011

Portanto, -5 em complemento de 2 é representado como 1011.

## Conclusão

Os sistemas de numeração são fundamentais para a eletrônica digital e a computação. O sistema binário é especialmente importante, pois é a base para a representação e manipulação de dados em sistemas digitais. A compreensão da conversão de bases, representação posicional e operações de deslocamento é essencial para o design e análise de circuitos digitais. A representação de números sinalizados em complemento de 2 permite a manipulação de números negativos em sistemas binários.

