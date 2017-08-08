# Enumeradores
_Enums_ definem um tipo comum para um grupo de valores relacionados e nos permitem utilizá-los de maneira segura no nosso código. Como são tipos definidos, o compilador irá nos apontar caso ocorra algum problema no momento de compilação.

As enumerações em Swift são muito flexíveis, não é necessário agregar um valor mas caso tenha um valor agregado pode ser string, caracter ou inteiros e pontos flutuantes. Também podemos associar um valor aos _casos_ enumerados, ele será armazenado juntamente com o _caso_ podendo ser extraído para uso quando necessário.

Os _enums_ também podem usar muitas funcionalidades que tradicionalmente são de uso exclusivo das _classes_ como:  propriedades, métodos, inicializadores, extensões e protocolos.

## Criação
```swift
enum Direcao {
    case norte
    case sul
    case leste
    case oeste
}

// Para usar basta selecionar o caso
let bussola: Direcao = Direcao.sul

// Quando o tipo está explicito, podemos usar simplesmente o _caso_
var d: Direcao = .leste
// inclusive nas alterações :)
d = .oeste



// Podemos listar todos ou alguns casos na mesma linha separados por virgulas.
enum Planeta {
    case mercurio, venus, terra, marte
    case jupiter, saturno, urano, netuno
}

let planetaX: Planeta = .jupiter
```

## Comparações
Para realizar comparações ou saber qual o _caso_ selecionado podemos usar `switch-case` e `if`:
```swift
switch d {
case .norte:
    print("Norte")

case .sul:
    print("Sul")

default:
    print("Outra direção")
}
// Repare que não precisamos listar todas as possibilidades do enum,
// se não entrar nos _casos_ que listamos o controle vai para o `default`

// Porém se listarmos **todos** os casos do enum podemos omitir o `default`
switch d {
case .norte, .sul:     // podemos listar múltiplos casos usando `,`
    print("vertical")

case .leste, .oeste:
    print("horizontal")
}



switch planetaX {
case .terra:
    print("praticamente inofensivo")

default:
    print("inseguro para humanos")
}

// também podemos checar o caso com `if`
if planetaX == .terra {
    print("palido ponto azul")
}
```

## Valores Agregados
Podemos agregar valores nos casos, com isso temos um mapa de valor para cada _caso_. Se o tipo for incrementável ele será automaticamente preenchido começando pelo zero, se for _String_ ela terá o mesmo valor do nome do _caso_.
```swift
enum DiaSemana: Int {
    case domingo = 1  // como o valor começa pelo zero, podemos atribuir um novo
    case segunda      // inicio e deixar o incrementador auto-preencher o demais
    case terca
    case quarta
    case quinta
    case sexta
    case sabado
}

// para acessar o valor usamos a propriedade `rawValue`
let numero = DiaSemana.sabado.rawValue
print(numero)



enum Mes: String {
    case janeiro, fevereiro, marco
    case abril, maio, junho
    case julho, agosto, setembro
    case outubro, novembro, dezembro
}

print(Mes.agosto.rawValue)



enum CaracterControleASCII: Character {
    case tab       = "\t"
    case novaLinha = "\n"
    case retorno   = "\r"
}

let nl = CaracterControleASCII.novaLinha.rawValue
print("Nova linha aqui ->\(nl)<-")
```

## Valores Associados
Diferente dos valores agregados -- que são definidos no momento de criação do enumerador -- os valores associados podem ser atribuídos posteriormente. Ótimos exemplos de valores associados são os [`Optionals`][gh-optional] da Swift ou a micro-biblioteca [`Result`][gh-result].
```swift
enum CodigoBarras {
    case upc(Int, Int, Int, Int)
    case qrCode(String)
}

var produto: CodigoBarras = .upc(8, 85393, 51226, 3)
produto = .qrCode("ABCDEFGHIJKLMNOP")



// Comparações:
//   Como agora temos um valor associado ao _caso_, podemos fazer a comparação e
//   extração usando `let`. Note que a extração só vai ocorrer se entrar no _caso_.
//
// - switch-case
switch produto {
case let .upc(sistemaNumerico, fabricante, produto, digito):
    print("UPC: \(sistemaNumerico), \(fabricante), \(produto), \(digito)")

case .qrCode(let codigo):
    print("QRCode: \(codigo)")
}

// - if-case
if case .qrCode(let codigo) = produto {
    print("QRCode: \(codigo)")
}
```

Como sempre não deixe de conferir a [documentação oficial][doc-enum] para mais informações e exemplos.

Até a próxima!
\>}

[doc-enum]: https://developer.apple.com/library/content/documentation/Swift/Conceptual/Swift_Programming_Language/Enumerations.html
[gh-optional]: https://github.com/apple/swift/blob/5d17b31948b0ff7132149e9e86f254e69328934e/stdlib/public/core/Optional.swift#L122-L133
[gh-result]: https://github.com/antitypical/Result
