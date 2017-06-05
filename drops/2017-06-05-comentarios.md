Comentários
===
Neste post vamos explorar um pouco sobre comentários.
Eles são importantes para documentar o código, porém não exagere na quantidade, preze pela qualidade e necessidade. Quem for ler depois de você agradecerá. 😀

Como funciona?
---
Na Swift temos duas maneiras de realizá-los:
1. Em linha
```swift
// tudo após as barras será comentado
// podemos usar para comentar linhas inteiras
let limite = 100 // ou adicionar comentários após o código
```
2. Em bloco
```swift
/*
	tudo entre os  delimitadores será comentado
	dessa forma podemos comentar blocos
	não importando quantas linhas
	serão utilizadas
*/
/* também podemos inserir no meio de um trecho */
let limite /* valor máximo */ = 100
/* mas perdemos muita legibilidade dessa forma */
```

Documentando seu código
---
Além de utilizar os comentários ao longo de seu código para facilitar o entendimento, podemos usá-los para documentar classes e funções, inclusive o Xcode interpreta e exibe no balão de documentação[^fn-popup-doc].

Para aproveitar dessa facilidade basta fazer os comentários com uma pequena modificação, usando três barras ou dois asteriscos:
```swift
/// usamos três barras nos comentários de linha
/** ou dois asteriscos
	nos comentários de bloco
*/
```

Exemplo:
```swift
/// Cria uma saudação com o nome da pessoa na forma de String.
///
/// - warning: Cuidado! Nem todos gostam de tanta atenção.
/// - parameter nome: nome da pessoa
/// - returns: string de saudação personalizada
func saudacao(nome: String) -> String {
	return "Olá \(nome), seja bem vindo!";
}
```
ou
```swift
/**
	Cria uma saudação com o nome da pessoa na forma de String.

	- warning: Cuidado! Nem todos gostam de tanta atenção.
	- parameter nome: nome da pessoa
	- returns: string de saudação personalizada
*/
func saudacao(nome: String) -> String {
	return "Olá (nome), seja bem vindo!";
}
```

Agora que já conhece todas as vantagens dos comentários é hora de colocá-los em prática, mas lembre-se: não exagere, comentários em excesso também podem ser um problema pois afetam a legibilidade do seu código.

Até a próxima!
\>}

[^fn-popup-doc]: Para acessar o balão de documentação basta segurar a tecla option (<kbd>&#8997;</kbd>) e clicar no método ou classe que deseja ver a documentação.
