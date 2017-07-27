# Date e DateFormatter
Seja para cadastrarmos a data do nosso aniversário ou o vencimento do cartão, é quase certo que em algum momento sua aplicação irá  trabalhar com datas. Para tal tarefa o Foundation possui [`Date`][doc-date] e [`DateFormatter`][doc-dateformatter] que são aliados poderosos para criação e formatação de datas.

[`Date`][doc-date] representa um ponto no tempo, independente de calendário ou fuso horário. É uma ponte para a [`NSDate`][doc-nsdate] e representa o tempo transcorrido relativo a uma data considerada absoluta -- 1 de Janeiro de 2001 00:00:00 UTC. Sua inicialização pode receber um [`TimeInterval`][doc-timeinterval], que é um `typealias` para `Double`.

## Criação
```swift
// Criando a data atual
let agora = Date()

// Criando uma data meia hora no futuro
let daquiUmaHora = Date(timeIntervalSinceNow: 60 * 30)
// Como o TimeInterval representa segundos, usamos 60 * 30
// para o total de segundos em meia hora (segundos * minutos)

// Criando uma data uma hora no passado
let umaHoraAtras = Date(timeIntervalSinceNow: -(60 * 60 * 1))
// Como o inicializador usa o momento atual de referência,
// usamos o valor negativo para representar tempo passado
// (segundos * minutos * horas)

let decada: TimeInterval = 60 * 60 * 24 * 365 * 10
// segundos * minutos * horas * dias * anos

let anos80 = Date(timeIntervalSince1970: decada)
// Repare que ao inspecionarmos o valor temos o seguinte resultado:
// 1979-12-30 00:00:00 +0000
//
// Isso acontece porque o Date não se apega a calendários, com isso **não**
// contabiliza anos bissextos. No nosso exemplo perdemos dois dias por causa disso.

// Usando um valor negativo, vamos para o passado.
// Aqui teremos o mesmo problema, nesse caso perdemos três dias.
let anos60 = Date(timeIntervalSince1970: -decada)
// 1960-01-04 00:00:00 +0000
```

## Comparações
```swift
// Podemos comparar datas
if anos80 > anos60 {
    print("Anos 80 vieram depois dos Anos 60")
}

if agora != umaHoraAtras {
    print("O tempo passou e eu nem vi!")
}
```

---

## DateFormatter
E quando precisamos formatar a data para uma exibição adequada e de acordo com a localização ou necessidade da aplicação?
Para esse tipo de tarefa que existe o [`DateFormatter`][doc-dateformatter]. Ele é responsável pela formatação da data -- tanto para exibição como leitura.

#### Exemplos
```swift
let formatador = DateFormatter()

// Podemos usar a região baseado no sistema
formatador.locale = Locale.current
// Ou específica
formatador.locale = Locale(identifier: "pt_BR")

// Estilo da formatação longo
formatador.dateStyle = .full
formatador.timeStyle = .full
formatador.string(from: agora)
// quinta-feira, 27 de julho de 2017 12:34:56 Horário Padrão de Brasília

// Ou curto
formatador.dateStyle = .short
formatador.timeStyle = .short
formatador.string(from: agora)
// 27/07/2017 12:34

// Somente formatação de tempo
formatador.dateStyle = .none
formatador.timeStyle = .medium
formatador.string(from: agora)
// 12:34:56

// etc

// Também podemos definir um formato específico caso os padrões não atendam a necessidade
formatador.dateFormat = "YYYY-MM-dd HH:mm"
formatador.string(from: agora)
// 2017-07-27 12:34
```

#### Transformanto Texto em Date
``` swift
// Podemos converter o de String para Date facilmente usando o DateFormatter
let nascimentoString = "1986-08-21"
formatador.dateFormat = "YYYY-MM-dd" // Lembre-se de acertar o formato antes!
let dataNascimento = formatador.date(from: nascimentoString)
// Optional(1986-08-21 03:00:00 +0000)
```
Usamos `pt_BR` neste exemplo, mas caso você queira utilizar outra localização dê uma olhada [nesta lista][locale-list].

## Guia de formatos
Abaixo listamos os principais formatos usados na propriedade `dateFormat` para facilitar a sua vida 😉:
- **EEEE**: Representação do dia da semana (Ex: Segunda-feira);
- **dd**: Representação do dia (Ex: 21);
- **MMMM**: Representação escrita do mês (Ex: Janeiro);
- **MMM**: Representação escrita simplificada do mês (Ex: Jan);
- **MM**: Representação numérica do mês (Ex: 01);
- **yyyy** ou **YYYY**: Representação do ano com os 4 dígitos (Ex: 1984);
- **yy** ou **YY**: Representação do ano com 2 dígitos (Ex: 84);
- **HH**: Representação da hora com dois dígitos (Ex: 19);
- **mm**: Representação dos minutos com 2 dígitos (Ex: 53);
- **ss**: Representação dos segundos com 2 dígitos (Ex: 40);
- **zzz**: TimeZone com 3 letras (Ex: GCM);

Trabalhar com datas não é tão difícil quando entendemos o que cada peça do quebra cabeça faz. Não deixe de consultar a documentação oficial de [Date][doc-date] e [DateFormatter][doc-dateformatter] caso tenha alguma dúvida.

Até a próxima 😁
\>}

[doc-date]: https://developer.apple.com/documentation/foundation/date
[doc-nsdate]: https://developer.apple.com/documentation/foundation/nsdate
[doc-dateformatter]: https://developer.apple.com/documentation/foundation/dateformatter
[doc-timeinterval]: https://developer.apple.com/documentation/foundation/timeinterval
[locale-list]: https://gist.github.com/jacobbubu/1836273
