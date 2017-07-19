# Strings
O tipo `String` representa uma série de caracteres, como "Olá, mundo!" ou "Andorinha". O conteúdo de uma `String` pode ser acessado de diversas maneiras, incluindo como uma coleção de `Character`s.

Foram projetadas para serem extremamente eficientes e compatíveis com o padrão [Unicode][].
A sintaxe para criação e manipulação é leve e legível, com uma forma literal[^fn-literal] similar a [linguagem C][clang]. A concatenação e mutabilidade são bem simples de serem realizadas e de forma bastante intuitiva, assim como a interpolação.

O tipo `String` pode ser convertido em `NSString` através do recurso de ponte ([bridge][]), porém como o `Foundation` extende e expõe os métodos definidos na versão `NS`, basta importá-lo que podemos acessar essas definições sem precisar de conversões.

## Criação
```swift
// forma literal
let texto = "Olá, mundo!"

// na Swift 4 também podemos usar a forma literal com múltiplas linhas
let bloco = """
    Ninho da Andorinha
    https://ninhodaandorinha.com.br
    """

// string vazia
let vazio = ""
// ou
let nada = String()
```

## Manipulação
```swift
// Mutabilidade
// para indicar que a string pode ser alterada basta usar var
var mensagem = "Olá"

// Concatenação
// para adicionar valores na string usamos o sinal +
mensagem = mensagem + ", "
// podemos simplificar a linha acima usando o operador +=
mensagem += "Mundo!"

// Interpolação
// para inserir valores no meio de uma string colocamos \()
// no local que a inserção deve ocorrer
let valor = 7
let descricao = "O dobro de \(valor) é: \(valor * 2)."
// Note que podemos inclusive executar expressões no local da inserção
```

## Algumas funcionalidades comuns
```swift
// verificar se uma String está vazia
let meuCarro = ""
if meuCarro.isEmpty {
    print("Você não tem um carro :(")
}

// percorrer caractere por caractere
for letra in "abcdef" {
    print(letra)
}

// total de caracteres
let documento = "AF302C-0"
print(documento.count)
```

Como deu para perceber, as `String`s além de serem um tipo bem comum em nossas aplicações, ainda possuem um amplo repertório de propriedades e funções que facilitam nossa vida. Existem muito mais possibilidades que não mencionamos não deixe de conferir a [documentação oficial][doc], por hora ficamos por aqui.

Até a próxima!
\>}

[Unicode]: https://pt.wikipedia.org/wiki/Unicode
[clang]: https://pt.wikipedia.org/wiki/C_%28linguagem_de_programação%29
[bridge]: https://developer.apple.com/library/content/documentation/Swift/Conceptual/BuildingCocoaApps/WorkingWithCocoaDataTypes.html#//apple_ref/doc/uid/TP40014216-CH6
[doc]: https://developer.apple.com/documentation/swift/string
[literal]: https://pt.wikipedia.org/wiki/Literal_(programação_de_computadores)

[^fn-literal]: Em ciência da computação, um literal é uma notação para representar um valor fixo no código fonte. [Ver mais][literal]
