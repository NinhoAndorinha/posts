Coleções: Array
===
A Swift possui três tipos básicos de coleções: _Array_[^fn-array],  _Dictionary_[^fn-dictionary] e _Set_[^fn-set]. Cada qual com funcionamento e aplicação específica porém todos são [fortemente tipados][wiki-ft] e armazenam uma **coleção** de valores.

O _Array_ -- também conhecido como [Arranjo ou Vetor][wiki-array] -- consiste em uma lista ordenada de valores do mesmo tipo, que podem ser acessados através de um índice.

Criação
---
```swift
// Quando criamos arrays diretamente por código podemos omitir o tipo dos elementos
let animais = [ "Cachorro", "Gato" ]

// Caso prefira, pode explicitar o tipo dos elementos da seguinte forma
var numerosDaSorte: [Int] = [ 4, 8, 15, 16, 23, 48 ]

// Array vazio
var numerosPrimos = [Int]()
// ou
var numerosFibonacci: [Int] = []

// Note que ao usarmos `let` nossos arrays são criados como constantes
// e **não** podem mais ser alterados. Para permitir a mutabilidade da coleção
// criamos usando `var`.
```

Manipulação
---
```swift
// Acessando valores por índice
// - leitura
animais[0]            // primeiro elemento
numerosDaSorte[2...4] // índices 2, 3 e 4
numerosDaSorte[3...]  // do índice 3 ao último
// - escrita
numerosDaSorte[5] = 42
numerosDaSorte[...2] = [ 1, 2, 3 ] // do primeiro ao índice 2

// Inserindo Valores
// - no fim
numerosPrimos.append(2)
numerosPrimos += [ 3 ]
numerosFibonacci.append(contentsOf: [ 2, 3 ])
numerosFibonacci += [ 5, 8, 13 ]
// - no indice
numerosPrimos.insert(1, at: 0)
numerosFibonacci.insert(contentsOf: [ 1, 1 ], at: 0)

// Removendo Valores
numerosPrimos.removeFirst()   // primeiro
numerosFibonacci.removeLast() // ultimo
numerosDaSorte.remove(at: 3)  // no indice
numerosDaSorte.removeAll()    // todos
```

Algumas funcionalidades comuns
---
```swift
// Total de elementos
animais.count

// Array vazio
numerosDaSorte.isEmpty

// Contém um determinado elemento
numerosPrimos.contains(4)

// Laço
for numero in numerosPrimos {
    print(numero)
}

// Laço com índice
for (indice, numero) in numerosFibonacci.enumerated() {
    print("O elemento [\(numero)] está na posição \(indice + 1).")
}
```

Não deixe de se aprofundar ainda mais lendo a [documentação oficial][doc-array].

Até a próxima!
\>}

[wiki-array]: https://pt.wikipedia.org/wiki/Arranjo_(computa%C3%A7%C3%A3o)
[wiki-dictionary]: https://pt.wikipedia.org/wiki/Vetor_associativo
[wiki-set]: https://pt.wikipedia.org/wiki/Conjunto_(tipo_de_dado_abstrato)
[wiki-ft]: https://pt.wikipedia.org/wiki/Linguagem_tipada#Linguagens_fortemente_tipadas
[doc-array]: https://developer.apple.com/library/content/documentation/Swift/Conceptual/Swift_Programming_Language/CollectionTypes.html#//apple_ref/doc/uid/TP40014097-CH8-ID107

[^fn-array]: Arranjo, variável indexada, vetor, matriz… [ver mais][wiki-array].
[^fn-dictionary]: Dicionário, vetor associativo, mapa… [ver mais][wiki-dictionary].
[^fn-set]: Conjunto, conjunto estático, conjunto congelado… [ver mais][wiki-set].
