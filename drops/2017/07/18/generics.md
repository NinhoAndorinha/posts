# Generics
Um [código genérico][wiki-generics] é um código que trabalha de forma abstrata, ganhando flexibilidade e evitando redundâncias. Boa parte da base da Swift é escrita utilizando generics, e essa é uma das razões da linguagem ser tão poderosa.

Um ótimo exemplo da utilização de generics na Swift é na utilização das _Coleções_. Já se perguntou como estes tipos aceitam elementos de tantos tipos diferentes? 🤔

```swift
// Declaramos um array de elementos do tipo Int,
// ou seja [Int] está implícito.
let idades = [ 10, 20, 10 ]
// [Int] na verdade é apenas uma maneira -- mais bonita -- de representar
// a forma natural: Array<Int>.
// Dessa forma temos explicitamente a representação da _coleção_ (Array)
// e do tipo do elemento (<Int>).

// Então podemos declaramos um array de elementos do tipo String dessa forma:
let nomes: Array<String> = [ "Merola", "Joselito", "Lucas" ]

// Nos dicionários, chave e valor são genéricos,
// neste caso definimos como String e Double
let pesos: Dictionary<String, Double> = [ "Joao": 86.9, "Carla": 54.2 ]
```

## Como Usar?
Para utilizar generics em nosso próprio código é bem simples, precisamos criar a representação de um tipo e quando precisar referenciá-lo, usar essa representação. Vamos imaginar que precisamos implementar uma [fila][wiki-fifo], e por simplicidade vamos usar um `Array` para armazenar os elementos.

Ao começarmos a implementar já nos deparamos com um problema:
```swift
class Fila {
    // Como a Swift nos obriga a colocar o tipo do elemento
    // aqui temos que falar o que vai nesse array.
    private var itens = [Int]()
}
```

Se não fosse pelo generics, iríamos ter que escrever praticamente o mesmo código para cada variação da nossa `Fila`, e acabaríamos com: `FilaInt`, `FilaString`, `FilaDouble`, etc.

#### Representação de um Tipo
```swift
class Fila<T> {  // Aqui fica a representação ou seja, no escopo da classe criamos
                 // uma forma de simbolizar um tipo que ainda não sabemos qual é.

    // Repare que agora o tipo é T, não sabemos qual será até a Fila ser utilizada.
    private var itens = [T]()
}
```

No exemplo anterior, utilizamos `T` para representar o tipo genérico do parâmetro. No entanto podemos utilizar uma nomenclatura descritiva com o contexto do que está sendo criado para facilitar o entendimento.
```swift
class Fila<Elemento> {
    private var itens = [Elemento]()
}
```

#### Exemplo
```swift
class Fila<Elemento> {
    private var itens = [Elemento]()

    func enfileira(_ item: Elemento) {
        itens.append(item)
    }

    func desenfileira() -> Elemento {
        return itens.remove(at: 0)
    }
}

// Usando a Fila:
let senha = Fila<Int>()
senha.enfileira(5)
senha.enfileira(9)

var proximo = senha.desenfileira()

// Com isso podemos rapidamente criar filas de qualquer tipo usando Fila<Tipo> :)
```

## Restringindo tipos
Podemos fazer com que nossos tipos genéricos se restrinjam a herdar de uma classe, protocolo ou um conjunto deles. Com isso, conseguimos dar um pouco mais especificidade para um tipo genérico sem ferir o seu conceito abstrato.

```swift
// Criamos uma função que recebe um tipo UIView ou descendente:
func adicionarAncora<V: UIView>(view: V) {
    // Adicionar constraints para uma view
}
// Repare que para usar generics em funções, o conceito é o mesmo ;)

let botao = UIButton()
adicionarAncora(view: botao)

let foto = UIImageView()
adicionarAncora(view: foto)

// Como nossa função recebe um tipo genérico restrito a UIView, se tentarmos
// usar algo diferente o compilador já detecta o erro:
let numero = 10.0
adicionarAncora(view: numero) // <- Erro



// Aceita apenas valores de tipos que permitam comparação de igualdade
func verificarIgualdade<Valor: Equatable>(valor1: Valor, valor2: Valor) -> Bool {
    return valor1 == valor2
}

verificarIgualdade(valor1: 10, valor2: 10)
verificarIgualdade(valor1: 3.14, valor2: 6.12)
verificarIgualdade(valor1: "alpha", valor2: "omega")
```

Ainda há muito o que falar sobre Generics, e com certeza voltaremos ao assunto.
Aproveite para se aprofundar lendo a [documentação oficial][doc-generics].

Até a próxima!
\>}

[wiki-generics]:https://pt.wikipedia.org/wiki/Programação_genérica
[wiki-fifo]: https://pt.wikipedia.org/wiki/FIFO
[doc-generics]: https://developer.apple.com/library/content/documentation/Swift/Conceptual/Swift_Programming_Language/Generics.html
