# Circuitos combinacionais

Após um exemplo inicial rápido, vamos criar um circuito combinacional para demonstrar mais funcionalidades da linguagem Verilog. O circuito que vamos criar é o do alerta de falta de cinto de segurança de um carro. 

## Primeira versão

!!! Especificação
    O circuito de alerta de falta de cinto de segurança do carro possui, como entrada, 4 sinais de entrada: sensor de cinto do banco do motorista (**motorista**), sensor de cinto do banco do carona (**carona**), que servem para indicar que os respectivos cintos de segurança estão travados (valor 1) ou soltos (valor 0), sensor da chave do carro ligada (**chave**) com valor 1 e 0 caso desligada, e peso no banco do carona (**peso**) indicando que existe alguém sentado no banco do carona quando o valor é 1. Note que não existe um sensor no banco do motorista pois essa situação já é coberta pela chave ligada. A saída do circuito (**alerta**) deve estar ativa (com valor 1) quando um dos cintos estiver solto e for necessário.

Ao pensar no circuito, a primeira opção para solucionar é montar a expressão lógica que indica o resultado do alerta. A expressão lógica é dada por:

alerta = chave E (motorista OU (carona E peso))

indicando que o alerta só toca se a chave estiver na ignição e se uma das duas demais condições for verdadeira: cinto do motorista solto ou cinto do carona solto e alguém sentado no banco do carona.

!!! Hardware
    O circuito que acabamos de descrever é um circuito combinacional. Ele é chamado assim pois a saída do circuito depende apenas das entradas do circuito. Não existe um estado interno que influencie a saída do circuito. O circuito é composto por portas lógicas que realizam operações lógicas sobre os sinais de entrada.

O circuito pode ser representado em Verilog da seguinte forma:

```verilog
module alertaCinto(
  input chave,
  input motorista,
  input carona,
  input peso,
  output alerta
);

  assign alerta = chave & (motorista | (carona & peso));

endmodule
```

O comando **assign** da linha 9 concentra todo o conhecimento do circuito, definindo que a saída **alerta** é igual a expressão lógica que está à direita do sinal de igual. A expressão lógica é a mesma que descrevemos anteriormente.

Você pode ter múltiplas saídas em um módulo e provavelmente terá várias expressões lógicas, uma para cada saída. O código acima é um exemplo de um módulo com apenas uma saída.

## Versão ampliada

Suponha agora que você também deva emitir um outro alerta, sobre porta aberta, caso a chave esteja ligada e a porta do carro esteja aberta. A expressão lógica para a saída **alertaChave** é dada por:

alertaChave = chave & porta

O código em Verilog para o módulo que contém as duas saídas é (o sintal alerta original foi trocado para alertaCinto para facilitar a leitura):

```verilog
module alertaCintoPorta(
  input chave,
  input motorista,
  input carona,
  input peso,
  input porta,
  output alertaCinto,
  output alertaChave
);

  assign alertaCinto = chave & (motorista | (carona & peso));
  assign alertaChave = chave & porta;

endmodule
```

## Crescendo o circuito um pouco mais

Um terceiro alerta pode ser instalado no carro para ser ativado apenas quando o carro estiver com uma das portas abertas e em movimento. Para isso, um sensor de movimento chamado **movimento** será adicionado à entrada com valor 1 quando o carro estiver se movendo, além disso, o sensor porta será dividido em 4 portas e, para isso, transformado em um vetor de 5 bits com a seguinte ordem: dianteira esquerda, dianteira direita, traseira esquerda, traseira direita e porta malas. A expressão lógica para a saída **alertaMovimento** é dada por:

alertaMovimento = movimento & |porta;

Note a existência do operador de redução | antes do **porta**. Esse operador realiza a operação OU sobre todos os bits do vetor **porta**. O código Verilog atualizado fica então como:

```verilog
module alertaVeiculo(
  input chave,
  input motorista,
  input carona,
  input peso,
  input [4:0] porta,
  input movimento,
  output alertaCinto,
  output alertaChave,
  output alertaMovimento
);

  assign alertaCinto = chave & (motorista | (carona & peso));
  assign alertaChave = chave & porta[0];
  assign alertaMovimento = movimento & |porta;

endmodule
```

A expressão para **alertaChave** foi atualizada para contar apenas com a porta do motorista como estava antes. O nome do módulo agora ficou para **alertaVeiculo** para conter, de forma genérica, todos os alertas emitidos.

## Conclusão

Neste capítulo, você viu como criar um circuito combinacional em Verilog. O circuito combinacional é um circuito digital que tem como saída uma função booleana das entradas. O circuito é composto por portas lógicas que realizam operações lógicas sobre os sinais de entrada. Não existe um estado interno que influencie a saída do circuito.

## Pratique

Não foram construídos testes para esse circuito, você consegue construir testes para cada um dos alertas para verificar se as expressões lógicas estão corretas?

1. Crie um módulo de teste para o circuito **alertaVeiculo**.
2. As vezes, colocar todas as expressões lógicas em um único componente pode complicar a legibilidade, o que não é o caso no nosso circuito pequeno. Você pode separar cada alerta em um módulo diferente e instanciá-los no módulo **alertaVeiculo**. Tente fazer isso.

