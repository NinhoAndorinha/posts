# Swift 4: Codable
Uma das novidades do Swift 4 foi a introdução do [arquivamento e serialização][swift-evo] de tipos nativos, com isso podemos salvar nossos tipos criados na Swift com `NSCoding` por exemplo. Porém a melhor parte é que também podemos utilizar o `NSPropertyListSerialization` e o `NSJSONSerialization` para transformar em **Property List** e **JSON** respectivamente.

Suponha que nosso modelo de dados é uma `struct` que representa uma temperatura, composta por valor e escala:
```swift
struct Temperatura {
    enum Escala: String {
        case celsius    = "°C"
        case fahrenheit = "°F"
    }

    var valor: Float
    var escala: Escala
}
```

Para podermos aplicar transformações em nossa estrutura precisamos conformar com o protocolo `Codable`. Como todos os tipos utilizados são nativos, só precisamos declarar a conformidade:
```swift
struct Temperatura: Codable {
    enum Escala: String, Codable {
```

Vamos aproveitar e criar uma lista de temperaturas para poder transformar mais tarde:
```swift
let previsao = [
    Temperatura(valor: 15, escala: .celsius),
    Temperatura(valor: 13, escala: .celsius),
    Temperatura(valor: 21, escala: .fahrenheit)
]
```

## Encoding
Agora que temos nosso modelo conformando com o protocolo `Codable` podemos transformá-lo em algum formato para armazenar em disco ou enviar à um servidor.

Uma das maneiras de armazenar em disco é com **Property List** e para isso usaremos o `PropertyListEncoder`:
```swift
let plistEncoder = PropertyListEncoder()

// como o formato padrão para escrita de plists é binário,
// vamos alterá-lo para ficar mais fácil de mostrar a transformação
// no código final essa linha pode ser removida
plistEncoder.outputFormat = .xml

let plistData = try plistEncoder.encode(previsao)
```

Nota: O método `.encode(_)` retorna um valor do tipo `Data`, portanto para ver o conteúdo de forma legível precisamos criar uma `String`:
```swift
print(String(data: plistData, encoding: .utf8))
```

Resultado:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<array>
	<dict>
		<key>escala</key>
		<string>°C</string>
		<key>valor</key>
		<real>15</real>
	</dict>
	<dict>
		<key>escala</key>
		<string>°C</string>
		<key>valor</key>
		<real>13</real>
	</dict>
	<dict>
		<key>escala</key>
		<string>°F</string>
		<key>valor</key>
		<real>21</real>
	</dict>
</array>
</plist>
```

Para transformar em **JSON** é só usar o `JSONEncoder`:
```swift
let jsonEncoder = JSONEncoder()

// como o formato padrão para escrita de JSON é compacto,
// vamos alterá-lo para ficar mais fácil de mostrar a transformação
// no código final essa linha pode ser removida
jsonEncoder.outputFormatting = .prettyPrinted

let jsonData = try jsonEncoder.encode(previsao)
```

Nota: O método `.encode(_)` retorna um valor do tipo `Data`, portanto para ver o conteúdo de forma legível precisamos criar uma `String`:
```swift
print(String(data: jsonData, encoding: .utf8))
```

Resultado:
```json
[{
	"valor": 15,
	"escala": "°C"
}, {
	"valor": 13,
	"escala": "°C"
}, {
	"valor": 21,
	"escala": "°F"
}]
```

## Decoding
Metade do trabalho já foi feito, transformamos tipos nativos para **plist** e **JSON**, agora vamos fazer o contrário. Isso vai facilitar muito a comunicação entre servidor e aplicativo, tornando o código mais simples e mais seguro. Para realizar a decodificação o _decoder_ precisa saber qual o tipo que deve tentar transformar, nesse caso `[Temperatura].self`, que representa uma lista de `Temperatura`s.

Para isso é só utilizar `PropertyListDecoder`:
```swift
let plistDecoder = PropertyListDecoder()
let plistDecoded = try plistDecoder.decode([Temperatura].self, from: plistData)
```

e `JSONDecoder`:
```swift
let jsonDecoder = JSONDecoder()
let jsonDecoded = try jsonDecoder.decode([Temperatura].self, from: jsonData)
```

## Exemplo Completo
```swift
//: Swift 4: Codable
//: ===
import Foundation

struct Temperatura: Codable {
    enum Escala: String, Codable {
        case celsius    = "°C"
        case fahrenheit = "°F"
    }

    var valor: Float
    var escala: Escala
}

let previsao = [
    Temperatura(valor: 15, escala: .celsius),
    Temperatura(valor: 13, escala: .celsius),
    Temperatura(valor: 21, escala: .fahrenheit)
]



//: Encoding
//: ---

//: - plist
let plistEncoder = PropertyListEncoder()
plistEncoder.outputFormat = .xml
let plistData = try plistEncoder.encode(previsao)
String(data: plistData, encoding: .utf8)

//: - JSON
let jsonEncoder = JSONEncoder()
jsonEncoder.outputFormatting = .prettyPrinted
let jsonData = try jsonEncoder.encode(previsao)
String(data: jsonData, encoding: .utf8)



//: Decoding
//: ---

//: - plist
let plistDecoder = PropertyListDecoder()
let plistDecoded = try plistDecoder.decode([Temperatura].self, from: plistData)

//: - JSON
let jsonDecoder = JSONDecoder()
let jsonDecoded = try jsonDecoder.decode([Temperatura].self, from: jsonData)
```

ou faça o [download do Playground][play].

Até a próxima!
\>}

[swift-evo]: https://github.com/apple/swift-evolution/blob/master/proposals/0166-swift-archival-serialization.md
[play]: /s/swift-4-codableplayground.zip
