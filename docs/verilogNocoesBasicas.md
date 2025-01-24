# Noções Básicas de Verilog

## Diferenças entre modelagem de hardware e linguagens de programação convencionais

Ao considerar a modelagem de hardware, é importante ter em mente que a modelagem de hardware é diferente da modelagem de software. A modelagem de software é feita em linguagens de programação convencionais, como C, C++, Java, Python, etc. A modelagem de hardware é feita em linguagens de descrição de hardware, como Verilog e VHDL. Em especial, é importante ter em mente que:

!!! Software
    Ao modelar um software (escrever um programa de computador), tem-se um processador como a unidade básica de execução, permitindo que o programador explore a execução ao longo do tempo. Como exemplo, o código abaixo

```c
main()
{
  int i, saida = 0;

  for (i = 0; i < 10; i++)
    saida += i;
}
```

pode ser executado passo a passo, como mostrado abaixo:

| i | saida |
|---|-------|
| 0 | 0     |
| 1 | 1     |
| 2 | 3     |
| 3 | 6     |
| 4 | 10    |
| 5 | 15    |
| 6 | 21    |
| 7 | 28    |
| 8 | 36    |
| 9 | 45    |

A variável **saida** tem seu valor alterado ao longo do tempo, que serão as iterações do laço **for** (de 0 a 9). A variável **i** também tem seu valor alterado ao longo do tempo, que serão as iterações do laço **for** (de 0 a 9). Dessa forma, basta ter um somador capaz de realizar a soma principal dentro do processador para que o programa funcione. Esse componente será utilizado tantas vezes quanto forem as iterações do laço for. (*nesse exemplo, não estamos tratando de processadores capazes de executar mais de uma instrução por vez, nem mesmo de múltiplos processadores. Nesses casos, ainda assim, a limitação da capacidade de execução em paralelo não fica a cargo do programador e sim do projetista de hardware.)

!!! Hardware
    Ao modelar um hardware, tem-se um ou mais circuitos digitais como as unidades básicas de execução, permitindo que o projetista explore a execução também ao longo do espaço. Como exemplo, o código abaixo

```verilog
module somador(
  input [3:0] a,
  input [3:0] b,
  output [3:0] soma
);

  assign soma = a + b;

endmodule
```

nesse caso, tem-se apenas um circuito capaz de realizar uma soma, sem o processo de iteração existente anteriormente com o laço **for**. Dessa forma, o circuito deve ser capaz de realizar a soma de todos os valores possíveis de **a** e **b**. Para a execução de uma sequência de somas como o exemplo anterior, uma alternativa seria ter um circuito com múltiplos somadores para realizar todas as somas necessárias simultaneamente. Outra alternativa de implementação seria ter um módulo que fosse gerando múltiplos valores para **a** e **b** e realizando a soma de dada par, permitindo que o circuito fosse executado ao longo do tempo. Entre as duas alternativas, existem soluções intermediárias que podem realizar mais de uma soma em paralelo, permitindo menor tempo de execução final. A escolha da melhor alternativa depende dos requisitos que o projetista deseja atender.

Uma implicação direta desse poder decisório está no fato de que os módulos (partes) dos componentes de hardware estarão em execução o tempo inteiro, ao contrário do software que tem uma modelagem predominantemente sequencial.

## Organizando o código em componentes/módulos

O conceito de modularidade é muito mais explícito quando estamos projetando hardware. Em especial, tudo que for desenvolvido em Verilog será um módulo. Dessa forma, é importante que o projetista tenha em mente que o código deve ser organizado em módulos, permitindo que o código seja reutilizado e que o projetista possa se concentrar em partes específicas do projeto.

Todo módulo se comunica com o exterior através de sinais, que podem ser de entrada, saída ou bidirecionais. Utilizando o exemplo de código acima do somador, os sinais **a** e **b** são de entrada e o sinal **soma** é de saída. A declaração dos sinais é feita na declaração do módulo.

Um módulo pode ser utilizado (denominamos instanciado) dentro de outro módulo, permitindo o reuso e melhor organização do código. Por isso, sempre que for definir um componente de hardware, é importante que o projetista pense em como esse componente será utilizado e como ele se comunica com o exterior para facilitar o reuso posterior.
