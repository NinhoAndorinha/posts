Constantes e Variáveis
===
Constantes e variáveis são formas de associar um nome a um valor, seja para armazenamento temporário, manipulação, operações, etc. São extremamente úteis para a programação e promovem um passo-a-passo no seu algoritmo.

O maior cuidado que temos que ter com elas são os nomes escolhidos, pois eles garantem a legibilidade e compreensão posterior. Depois precisamos decidir qual utilizar: variável ou constante?

Constantes
---
Como o próprio nome diz, uma vez atribuído um valor para uma constante, não podemos alterá-lo.
```swift
let limiteJogadores = 10 // número máximo de jogadores por sala
```

Variáveis
---
Ao contrário das constantes, aqui podemos alterar o valor sempre que necessário. Nossa única preocupação será com o tipo do valor[^fn-tipos].
```swift
var numeroJogadores = 0 // número atual de jogadores na sala
```

Exemplo:
```swift
let limiteJogadores = 10 // número máximo de jogadores por sala
var numeroJogadores = 0  // número atual de jogadores na sala

// ao entrar e sair jogadores podemos atualizar o valor da variável
numeroJogadores = 3

// note que estamos sempre utilizando o mesmo tipo de valor
// nesse caso um número
numeroJogadores = 1
```

Agora que conhecemos as diferenças básicas entre constantes e variáveis[^fn-ponteiros] podemos tomar uma decisão melhor quando for utilizá-las. Sempre que souber que um valor atribuído não será alterado, use uma constante. Via de regra, devido às otimizações de performance, erre para o lado da constante, melhor futuramente perceber que vamos precisar de uma variável e alterar do que lembrar de voltar atrás e usar a constante.

Até a próxima!
\>}

[^fn-tipos]: Como a Swift é uma linguagem [fortemente tipada](https://pt.wikipedia.org/wiki/Linguagem_tipada), uma vez que uma variável tem um tipo de valor definido todos os valores atribuídos posteriormente precisão ser do mesmo tipo.
[^fn-ponteiros]: Existem alguns outros pequenos detalhes entre elas, porém eles serão melhor explicados futuramente.
