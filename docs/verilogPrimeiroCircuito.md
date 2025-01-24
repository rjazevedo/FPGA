# O primeiro circuito

Nessa aula, veremos o primeiro circuito em Verilog e as principais partes do código necessárias para a correta modelagem e síntese do circuito.

!!! Dica
    Muitos materias e cursos sobre Verilog começam montando circuitos baseados em portas lógicas básicas tentando modelar os primeiros circuitos que um aluno encontra numa disciplina de circuitos lógicos. Apesar da abordagem interessante do ponto de vista da sequencialidade, ela não será utilizada nesse curso que irá tirar proveito da capacidade das ferramentas de hardware de realizar síntese de circuitos mais complexos a partir de descrições mais simples. 

## Um somador de 4 bits

O primeiro circuito que iremos modelar é um somador de 4 bits. Para isso, vamos utilizar o código abaixo:

![Circuito somador de 4 bits](img/somador.drawio.svg)

```verilog
module somador(
  input [3:0] a, // entrada de 4 bits
  input [3:0] b, // entrada de 4 bits
  output [3:0] soma // saída de 4 bits
);

  assign soma = a + b; // soma dos dois sinais de entrada

endmodule
```

As primeiras linhas do código declaram o módulo **somador** e as entradas e saídas do módulo. Nesse caso, temos duas entradas de 4 bits (**a** e **b**) e uma saída de 4 bits (**soma**). Note também a sintaxe de colocar cada sinal separado por vírgula e terminar a linha com ponto e vírgula. Você pode declarar toda a definição de um módulo em uma única linha mas procure tomar cuidado com legibilidade do código.

!!! Dica
    A declaração de entradas e saídas é feita utilizando o formato de vetor. No caso, o vetor é declarado utilizando o formato **[3:0]**, indicando que o vetor tem 4 bits. O formato **[3:0]** indica que o bit mais significativo é o bit 3 e o bit menos significativo é o bit 0. Dessa forma, o vetor **a** tem os bits **a[3]**, **a[2]**, **a[1]** e **a[0]**. O mesmo vale para o vetor **b** e **soma**. A forma recomendada de representar vetores é sempre com o bit mais significativo sendo o índice de maior valor e utilizar o menos significativo como zero.

A seguir, tem a linha iniciada com **assign** que serve para atribuir um valor a um sinal. Nesse caso, o sinal **soma** recebe o valor da soma dos sinais **a** e **b**. Note que o sinal **soma** foi declarado anteriormente como saída do módulo. É importante respeitar a direção dos sinais (entrada ou saída) para que a ferramenta de síntese consiga gerar o circuito corretamente.

!!! Dica
    A linha **assign** é utilizada para atribuir um valor a um sinal. O operador **=** é utilizado para atribuir um valor a um sinal. Já o operador **==** é utilizado para comparar dois valores.

Ao final, o circuito encerra com a palavra **endmodule**. Essa palavra é utilizada para indicar o final do módulo. Note que o módulo **somador** foi iniciado com a palavra **module**. Essa palavra é utilizada para iniciar a definição de um módulo.

## Verificando o circuito

Toda vez que um componente for implementado, é importante garantir o funcionamento e isso pode ser feito através do processo de verificação do circuito. No ciclo de desenvolvimento de hardware, os termos verificação e teste têm significados diferentes, ficando verificação para o processo de garantir a funcionalidade em simulação e teste para garantir a funcionalidade física. Apesar da diferença conceitual, você pode ouvir tanto verificação quanto testes em certos momentos como sinônimos.

!!! Dica
    O processo de verificação é muito importante no desenvolvimento de hardware pois permite que o projetista tenha confiança no circuito que está sendo desenvolvido. O processo de verificação é muito mais complexo que o processo de desenvolvimento do circuito e pode ser responsável por mais de 70% do tempo de desenvolvimento.

Para realizar a verificação do circuito, vamos utilizar o código abaixo (está longo, mas bem repetitivo no final):

```verilog
module tb_somador;

  reg [3:0] a, b; // registradores auxiliares a e b 
  wire [3:0] soma; // sinal extra para coletar o resultado

  somador uut(
    .a(a),
    .b(b),
    .soma(soma)
  );

  initial begin
    $monitor("a = %b, b = %b, soma = %b", a, b, soma);
    a = 0;
    b = 1;
    #1;
    a = 2;
    b = 3;
    #1;
    a = 6;
    b = 8;
    #1;
    a = 10;
    b = 5;
    #1;
    a = 8;
    b = 8;
    #1;
    a = 0;
    b = 0;
    #1;
    a = 15;
    b = 1;
    #1;
    a = 9;
    b = 8;
    #1;
    $finish;
  end;
endmodule
```

Note que o código para verificação é maior que o código para implementar o circuito. Isso é normal pois o processo de verificação é mais complexo que o processo de implementação. O código de verificação é composto por um módulo que é o módulo de testbench (tb_somador) e um módulo que é o módulo que está sendo testado (uut). O módulo de testbench é responsável por gerar os sinais de entrada e verificar os sinais de saída. O módulo que está sendo testado é o circuito que está sendo desenvolvido.

!!! Dica
    O módulo de testbench é um módulo que tem como objetivo testar o circuito que está sendo desenvolvido. O módulo de testbench é responsável por gerar os sinais de entrada e verificar os sinais de saída. O módulo que está sendo testado é o circuito que está sendo desenvolvido.

Nesse momento, novos elementos apareceram na descrição. Começando do início, temos a declaração de dois registradores auxiliares **a** e **b**. Esses registradores serão utilizados para gerar os sinais de entrada do circuito. Note que os registradores auxiliares são declarados como **reg**. O tipo **reg** é utilizado para declarar sinais que serão utilizados como registradores. O tipo **wire** é utilizado para declarar sinais que serão utilizados como fios. Entraremos em detalhes sobre as diferenças mais a frente. Por enquanto, basta saber que os sinais de entrada são registradores e os sinais de saída são fios. É possível utilizar os mesmos nomes dos sinais do módulo somador e no testbench pois são dois domínios diferentes. Essa é uma prática comum para facilitar a legibilidade.

O próximo trecho do código declara um módulo **somador** e faz a conexão da interface de entrada e saída com os sinais locais. Note que a conexão é feita utilizando o formato **.nome_interno(nome_externo)**. Esse formato é utilizado para indicar que o sinal local **nome_externo** está conectado ao sinal do módulo **somador** com o **nome_interno**. Como múltiplas cópias do mesmo módulo podem ser instanciadas, cada uma delas ganha um nome. Nesse caso, o nome é **uut** (*unit under test*).

O último trecho de código do módulo refere-se ao processo **initial** que vai desde o **begin** até o **end**. Ele serve para indicar um trecho de código Verilog que será executada sequencialmente e, normalmente, é utilizado para implementar a verificação. A primeira linha do processo **initial** é o comando **$monitor** que serve para monitorar os sinais. Nesse caso, o comando **$monitor** está monitorando os sinais **a**, **b** e **soma** e imprimindo os valores em binário. Isso significa que ele não será utilizado no circuito final e só será utilizado para a verificação. A sintaxe detalhada desse comando será vista posteriormente. Por hora, note a semelhança com o **printf** da linguagem C (embora não seja idêntico).

!!! Dica
    O comando **$monitor** é um comando de simulação e não é sintetizável. Isso significa que ele não será utilizado no circuito final e só será utilizado para a verificação. Tipicamente, coloca-se dentro do **initial** uma sequência de comandos não sintetizáveis para fazer a verificação do módulo de hardware.

Em seguida, tem-se trechos de 3 linhas atribuindo valores aos registradores **a** e **b** seguidos de um comando especial para avançar uma unidade tempo de simulação (**#1**). O número 1 é arbitrário nesse caso e poderíamos utilizar outros números para avançar. Como não estamos tratando de temporização no momento, basta avançar uma unidade de tempo que será suficiente. 

Ao executar os dois códigos (somador e testbench), o resultado será o seguinte:

```
a = 0000, b = 0001, soma = 0001
a = 0010, b = 0011, soma = 0101
a = 0110, b = 1000, soma = 1110
a = 1010, b = 0101, soma = 1111
a = 1000, b = 1000, soma = 0000
a = 0000, b = 0000, soma = 0000
a = 1111, b = 0001, soma = 0000
a = 1001, b = 1000, soma = 0001
```

Veja que as saídas refletem os valores inseridos no sistema e os resultados calculados pelo somador. Essa forma básica de verificação está, no fundo, apenas imprimindo as entradas e saídas e solicitando que o projetista verifique um a um, o que não é algo tão promissor para o caso de circuitos maiores. Posteriormente faremos algo mais elaborado nessa direção. Por hora, podemos saber que esse código aparenta estar correto verificando manualmente as respostas que estão corretas.

!!! Dica
    O processo de verificação deve ser mais elaborado que apenas imprimir os valores de entrada e saída. O processo de verificação deve ser capaz de verificar se o circuito está funcionando corretamente. Para isso, é necessário ter um conjunto de testes que cubra todas as possibilidades de entrada e saída. Para circuitos mais complexos, é comum utilizar ferramentas de verificação mais elaboradas.

!!! exercise choice "Pergunta"
    Qual é o valor correto, segundo esse circuito, para a soma de 10 + 8?

    - [ ] 18
    - [ ] 17
    - [ ] 16
    - [ ] 15
    - [ ] 14
    - [ ] 4
    - [ ] 3
    - [X] 2
    - [ ] 1
    - [ ] 0

    !!! answer
        O valor correto para a soma de 10 + 8 deveria ser 18 (10010), mas o somador só trabalha com números de 4 bits, portanto a resposta será 2, que equivale aos 4 bits menos significativos do valor 18. 

