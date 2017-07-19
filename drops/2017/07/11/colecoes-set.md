# Coleções: Set
O tipo _Set_ -- conhecido na ciência da computação como [Conjunto][wiki-set] -- consiste em uma lista de valores do mesmo tipo que não possuem ordenação e que não se repetem.

Isso significa que ao adicionarmos dois valores iguais em uma variável do tipo Set, apenas um entrará na coleção. O tipo _Set_ aceita apenas elementos que conformam com o protocolo [`Hashable`][doc-hashable] -- para que possa ser feita a comparação de igualdade.

## Criação
```swift
// Para declararmos uma variável Set, precisamos explicitar seu tipo
// Caso contrário, ela será criada como um array.
var amigosUnicos: Set = [ "José", "João", "Teobaldo", "Wallace", "Bruno" ]

//ou
let primos: Set<Int> = [ 2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 47 ]
```

## Manipulação
```swift
// Inserindo um valor
sobrenomes.insert("Cissoto")

// Removendo um valor
idades.remove(21)

// Ao tentar adicionar um valor que já existe, a quantidade de valores se mantém
idades.insert(10)


//Verificando existência de valores
if amigosUnicos.contains("Teobaldo") {
    print("Teobaldo é meu amigo")
}

// Acessando valores
for sobrenome in sobrenomes {
    print("Pessoas podem tem o sobrenome \(sobrenome)")
}
```

## Trabalhando com Conjuntos
```swift
let rock: Set = [ "U2", "Metallica", "Korn", "Foo Fighters", "Raimundos" ]
let popRock: Set = [ "Paralamas do Sucesso", "U2", "Skank" ]

// Cria um set com a união dos elementos dos sets
let tudoJunto = rock.union(popRock)
// {"Paralamas do Sucesso", "Metallica", "Foo Fighters", "Skank", "Korn", "Raimundos", "U2"}

// Cria um set com a interseção dos sets
let rockEPop = rock.intersection(popRock)
// {"U2"} -- somente elementos pertencentes aos dois sets

// Cria um set com os  não contidos no set fornecido
let somenteRock = rock.subtracting(popRock)
// {"Korn", "Metallica", "Raimundos", "Foo Fighters"}

// Cria um set com apenas as diferenças entre os sets
let estilosDiferentes = popRock.symmetricDifference(rock)
// {"Paralamas do Sucesso", "Metallica", "Skank", "Foo Fighters", "Korn", "Raimundos"}
```

## Algumas funcionalidades comuns
```swift
// Verifica se está vazio
sobrenomes.isEmpty

// Quantidade de elementos
idades.count

// Verifica se é um subset (está contido)
idades.isSubset(of: 1...100)

// Verifica se é um superset (contem)
idades.isSuperset(of: 1...100)
```

Não deixe de se aprofundar ainda mais lendo a [documentação oficial][doc-set].

Até a próxima!
\>}

[wiki-set]: https://pt.wikipedia.org/wiki/Conjunto_(tipo_de_dado_abstrato)
[doc-hashable]: https://developer.apple.com/documentation/swift/hashable
[doc-set]: https://developer.apple.com/documentation/swift/set
