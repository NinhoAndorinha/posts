# Testes Unitários: Introdução
Atualmente se fala muito sobre testes no desenvolvimento de aplicativos móveis. Unitários, de Interface, <abbr title="Test Driven Development">TDD</abbr>, etc. Mas o que são e como implementá-los?

Durante os anos iniciais do iOS era muito difícil ver algum projeto com testes. O motivo? Talvez pela falta de integração no Xcode, falta de bibliotecas, falta de ferramentas, ou apenas falta de costume do desenvolvedor.

Felizmente os tempos mudaram, temos cada vez mais aplicativos e bibliotecas usando testes hoje em dia.

## Por que Testar?
A resultado mais importante dos testes é saber se o que foi feito funciona. Além disso, conseguimos diminuir o número de **defeitos** e **falhas** presentes na aplicação. Como consequência a qualidade do produto melhora.

Um [estudo][study-camb] feito em 2013 pela Universidade de Cambridge mostra que o custo global das **falhas** é de 312 bilhões de dólares por ano. Também foi constatado que em média 50% do tempo dos desenvolvedores é gasto na **depuração e correção de falhas**.

Um [outro estudo][study-nist], feito em 2002 pelo <abbr title="National Institute of Standards and Technology">NIST</abbr> estimou que mais de um terço do valor gasto **corrigindo falhas** poderia ser economizado caso fossem realizados **investimentos em uma melhor infraestrutura de testes**.

#### O que são Defeitos e Falhas?
- _Defeito_ é um problema ou não conformidade sobre algo que foi especificado formalmente e deveria funcionar da maneira a qual foi descrita. Ou seja, enquanto seu código não atende ao especificado você tem um defeito.

- _Falha_ é um problema que não foi formalmente especificado, muitas vezes pode indicar um erro no projeto do produto. As falhas são os famosos [bugs][wiki-bug].

#### Modelo em V
Cada etapa do processo de desenvolvimento tem sua respectiva fase de teste:

![Modelo em V][01-vmodel]

> O <abbr title="Quality Assurance">QA</abbr> não é a primeira barreira para achar problemas, é a última!

---

## Testes Unitários
Escritos pelo desenvolvedor, os testes unitários testam a unidade -- menor parte -- de código. Ou seja, basicamente são testados métodos e estado de propriedades.

Além de serem uma boa prática, um projeto com testes unitários permite que os desenvolvedores realizem refatorações sem medo e façam [testes de regressão][wiki-regression] nas atualizações.

#### Escrevendo Código Testável
Para facilitar a adoção de testes unitários seu código deve estar bem arquitetado, com o tempo e experiência esse processo fica praticamente automático. Antes de escrever você já vai estar pensando em como vai testar, ou talvez até esteja usando uma metodologia com foco em testes -- como o <abbr title="Test Driven Development">TDD</abbr>.

Se ainda não tem o costume de testar não se preocupe, segue algumas dicas para começar a escrever código testável:
- **Uma tarefa**: quando estiver escrevendo funções e métodos, procure deixá-los com apenas uma tarefa. Caso tenha mais de uma, separe em outro componente;
- **Uma responsabilidade**: o mesmo conceito se aplica nas instâncias, deixe-as com apenas uma responsabilidade;
- **Extração, Extração, Extração!**: lembre-se que quanto mais _unidades_ de código tiver, mais fácil testar;
- **Não duplique código**: código duplicado gera testes duplicados;
- **Injete dependências**: ao invés de criar e usar as dependências dentro de algum componente, procure injetá-las. Vai ser mais fácil de testar e seu componente vai ficar mais modular.

#### O que testar?
Via de regra: tudo. Quanto mais testes melhor certo? Mais ou menos, a **qualidade** do teste também é muito importante.

O objetivo dos testes é passar **confiança** quando modificamos algo no projeto, se os testes não foram bem feitos que confiança teremos?

Procure pelo menos criar testes para todas as funcionalidades básicas. Por exemplo, em um projeto de _Calculadora_ as **operações** devem ser o foco da maioria dos testes, já que são a base de uma calculadora.

---

## Testes no Xcode
Caso esteja criando um projeto novo, basta selecionar o _checkbox_ para incluir os Testes Unitários (Include Unit Tests):

![Xcode Unit Test][02-checkbox]

Isso basicamente faz o Xcode criar um _Target_ para testes:

![Xcode Target][03-target]

 Portanto caso seu projeto não tenha sido criado assim, é só adicionar um novo _Target_ de testes `File > New > Target`:

![Xcode Add Target][04-add-target]

#### Código
Repare que agora temos uma nova pasta no projeto, no nosso exemplo `ContadorTests`, dentro dessa pasta ficam os arquivos com os testes. O primeiro já foi automaticamente criado pelo Xcode, `ContadorTests.swift`:
```swift
import XCTest              // Inclui biblioteca de testes do Xcode.
@testable import Contador  // Importa o bundle do projeto de maneira testável,
                           // com isso podemos testar componentes com controle
                           // de acesso _internal_.

class ContadorTests: XCTestCase {

    override func setUp() {
        super.setUp()
        // Método usado para construção e preparação.
        // Esse método é chamado **antes de cada** método de teste da classe.
    }

    override func tearDown() {
        // Método usado para desconstrução.
        // Esse método é chamado **depois de cada** método de teste da classe.
        super.tearDown()
    }

    func testExample() {
        // Exemplo de um método de teste.
        // Aqui usamos asserções (XCTAssert) para verificar que o teste
        // produz resultados corretos.
    }

    func testPerformanceExample() {
        // Exemplo de um método de teste de performance.
        self.measure {
            // Aqui colocamos o código que queremos medir o tempo gasto.
        }
    }
}
```

---

## Exemplo
Vamos criar um componente _Contador_ e testá-lo, as operações básicas do nosso contador são: **incrementar** e **zerar**:
```swift
class Contador {
    private(set) var total = 0  // private(set) quer dizer que só a classe Contador
                                // pode alterar o valor da propriedade.
    func incrementar() {
        total += 1
    }

    func zerar() {
        total = 0
    }
}
```

#### Construção e Destruição
Para começar a testar nosso _Contador_ vamos criar uma propriedade para armazenar uma instância e atribuir um contador nos métodos de `setUp()` e `tearDown()`:
```swift
class ContadorTests: XCTestCase {

    var c: Contador!  // Como estamos atribuindo o valor no `setUp()` e não no
                      // `init()` a propriedade tem que ser opcional, mas podemos
                      // usar `!` para deixar a propriedade desempacotada por padrão.

    override func setUp() {
        super.setUp()
        // Criando o contador aqui cada método de teste irá usar um novo contador,
        // isso faz com que o estado seja sempre novo, garantindo que não teremos
        // acumulação de algum estado que pode fazer com que testes falhem ou passem
        c = Contador()
    }

    override func tearDown() {
        // destrói o contador após o teste
        c = nil
        super.tearDown()
    }
}
```

#### Asserções
Agora podemos criar um teste para validar o funcionamento do nosso componente. Para isso usamos asserções, ou `XCTAssert`s.
Temos as seguintes possibilidades de validação:
- **XCTAssert**: resultado é verdadeiro (equivalente a `XCTAssertTrue`);
- **XCTAssertTrue**: resultado é verdadeiro;
- **XCTAssertFalse**: resultado é falso;
- **XCTAssertEqual**: dois valores são iguais;
- **XCTAssertEqualWithAccuracy**: dois valores são iguais de acordo com um fator de precisão;
- **XCTAssertNotEqual**: um valor é diferente de outro;
- **XCTAssertNotEqualWithAccuracy**: dois valores são diferente de acordo com um fator de precisão;
- **XCTAssertGreaterThan**: um valor é maior que o outro;
- **XCTAssertGreaterThanOrEqual**: um valor é maior ou igual que o outro;
- **XCTAssertLessThan**: um valor é menor que o outro;
- **XCTAssertLessThanOrEqual**: um valor é menor ou igual que o outro;
- **XCTAssertNil**: resultado é nulo;
- **XCTAssertNotNil**: resultado não é nulo;
- **XCTAssertThrowsError**: um erro foi lançado;
- **XCTAssertNoThrow**: um erro não foi lançado;
- **XCTFail**: falha imediatamente (útil para condicionais, ex: `guard` ou `if-else`);

#### Validações
Vamos começar criando um método de teste para validar o `incrementar()`, sabemos que toda vez que ele é chamado o valor do contador deve incrementar.
```swift
func testIncremento() {
    // Logo antes desse método ser chamado o `setUp()` irá criar um novo contador
    // então podemos testar se o valor inicial é zero.
    XCTAssertEqual(c.total, 0, "contador deve inicializar com total 0")

    // Vamos incrementar o valor e verificar novamente
    c.incrementar()
    XCTAssertEqual(c.total, 1, "após incremento, devemos estar em 1")

    // Note que podemos ter múltiplas validações por método, só cuidado para não
    // abusar e acabar testando muito mais que a **unidade**
    c.incrementar()
    c.incrementar()
    c.incrementar()
    XCTAssertEqual(c.total, 4, "após 3 incrementos, devemos estar em 4")
}
```

Seguindo o mesmo conceito, vamos testar a funcionalidade `zerar()`.
```swift
func testZerar() {
    XCTAssertEqual(c.total, 0, "contador deve inicializar com total 0")

    c.incrementar()
    c.zerar()
    XCTAssertEqual(c.total, 0, "após zerar, devemos estar com total 0")

    c.incrementar()
    c.incrementar()
    c.incrementar()
    c.zerar()
    XCTAssertEqual(c.total, 0, "após zerar, devemos estar com total 0")
}
```

Com isso temos as funcionalidades básicas de nosso _Contador_ testadas, caso seja necessário alguma refatoração ou mudança no código os testes devem garantir o funcionamento do componente.

Para executar os testes é só clicar e segurar no `Play` até aparecer `Test`, ou no menu `Product > Test`, ou ainda usando o atalho <kbd>&#8984; + U</kbd>.

![Xcode Test Report][05-report]

---

## Conclusões
Testar um aplicativo é uma tarefa muito importante, os Testes Unitários podem ajudar -- e muito -- nesse processo. Lembre-se de prezar sempre pela **qualidade** dos testes e do código!

Não deixe de conferir a [documentação oficial][link-doc] para mais informações sobre testes.
Assista também [essa palestra][link-wwdc] da **#WWDC17** dedicada a testes.

Até a próxima!
\>}

[wiki-bug]: https://pt.wikipedia.org/wiki/Falha_(tecnologia)
[wiki-regression]: https://pt.wikipedia.org/wiki/Teste_de_regressão
[study-camb]: http://www.prweb.com/releases/2013/1/prweb10298185.htm
[study-nist]: www.nist.gov/document/report02-3pdf
[link-doc]: https://developer.apple.com/documentation/xctest
[link-wwdc]: https://developer.apple.com/videos/play/wwdc2017/414/

[01-vmodel]: /img/tutoriais/2017/07/15/testes-unitarios-introducao/01-vmodel.png
[02-checkbox]: /img/tutoriais/2017/07/15/testes-unitarios-introducao/02-checkbox.png
[03-target]: /img/tutoriais/2017/07/15/testes-unitarios-introducao/03-target.png
[04-add-target]: /img/tutoriais/2017/07/15/testes-unitarios-introducao/04-add-target.png
[05-report]: /img/tutoriais/2017/07/15/testes-unitarios-introducao/05-report.png
