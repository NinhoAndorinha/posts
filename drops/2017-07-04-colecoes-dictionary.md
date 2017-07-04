# Coleções: Dictionary
O Dicionário -- conhecido também como [vetor associativo][wiki-dictionary] -- é um tipo de coleção que contém pares chave---valor. Não possui ordenação e cada chave acessa o valor diretamente associado a ela.

Tanto _chave_ quanto _valor_ tem seus tipos definidos no momento da criação do dicionário.

## Criação
```swift
// A representação de um _Dictionary_ é semelhante ao _Array_,
// para representar o conjunto chave--valor usamos `:`
let ninho = [ "linguagem": "swift" ]

let pessoa = [
    "nome": "Claudio",
    "sobrenome": "Farias",
    "nacionalidade": "Brasileiro"
]

// Podemos explicitar os tipos
var produtos: [Int: String] = [
    2041: "Camiseta Vermelha",
    3872: "Calça Azul",
    3018: "Regata branca"
]

// Dictionary vazio
var numerosChamada = [Int: String]()
// ou
var imagens: [String: NSURL] = [:]
```

## Manipulação
```swift
// Acessando _valores_ através da _chave_
pessoa["nome"]
produtos[3872]

// Como podemos tentar acessar uma _chave_ que não contém _valor_, o retorno vem
// empacotado em um _Optional_.
print(pessoa["nome"]) // imprime "Optional("Claudio")"

// Desempacotamos o _valor_
if let produto = produtos[2041] {
    print("O produto é \(produto)")
} else {
    print("Este produto não existe no nosso catálogo")
}

// Valores padrão e desempacotamento
// Caso a _chave_ tenha um _valor_ atribuído será retornado desempacotado, senão
// temos como retorno o valor padrão.
ninho["url", default: "https://ninhodaandorinha.com.br"]

// Adicionando elementos
imagens["gif"] = "http://gph.is/2cxrElv"

// Removendo elementos
produtos[3018] = nil
//ou
produtos.removeValue(forKey: 3018)

// Removendo todos os elementos.
imagens.removeAll()
```

## Funcionalidades comuns
 ```swift
 // Total de elementos
imagens.count

// Verifica se o dicionário está vazio
produtos.isEmpty

// Contém um determinado elemento utilizando uma operação
pessoa.contains { key, value in
    return value == "Farias"
}

// Percorrendo o dicionário
for (codigo, produto) in produtos {
    print("O código \(codigo) é do produto \(produto)")
}

// Apenas as chaves
for chave in pessoa.keys {
    print("A pessoa tem \(chave)")
}

// Apenas os valores
for nome in numerosChamada.values {
    print("O aluno \(nome) está na chamada!")
}
```

**Dica**
> Procure deixar as chaves dos seus dicionários em arquivos de configuração para facilitar no caso de mudanças.

Não deixe de se aprofundar ainda mais sobre dicionários lendo a [documentação oficial][doc-dictionary].

Até a próxima!
\>}

[wiki-dictionary]: https://pt.wikipedia.org/wiki/Vetor_associativo
[doc-dictionary]: https://developer.apple.com/documentation/swift/dictionary
