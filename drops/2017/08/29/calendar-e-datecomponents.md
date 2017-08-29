# Calendar e DateComponents
Não é incomum precisarmos realizar cálculos utilizando datas ou informações de um calendário, extraindo componentes como: dia, mês, ano e etc. Felizmente isso é possível utilizando [Calendar][doc-calendar] em conjunto com [DateComponents][doc-datecomponents].

A estrutura [Calendar][doc-calendar] nos fornece uma relação entre um calendário específico e um ponto absoluto no tempo (`Date`). Ela também nos fornece recursos para realizarmos cálculos, extrair componentes e outras funcionalidades a partir dessa relação.

Sua inicialização pode receber um [enumerador][ninhoreference-enum] que representa um [identificador de um calendário específico][doc-calendaridentifier], mas também podemos inicializar com as informações já fornecidas pelo usuário ao sistema operacional.

## Inicialização
```swift
// especificando um calendário
let calendario  = Calendar(identifier: .japanese)

// calendário selecionado atualmente no dispositivo (não monitora se o usuário alterar o calendário)
let calendarioUsuario = Calendar.current

// calendário atualizado do usuário (detecta alterações do usuário e atualiza o calendário)
let calendarioAtualizado = Calendar.autoupdatingCurrent
```

## Outras Funcionalidades
```swift
// `Locale` do calendário do usuário
calendario.locale

// fuso horário
calendarioUsuario.timeZone

// símbolos de AM E PM baseado no `Locale`
calendarioAtualizado.amSymbol   // => "AM"
calendarioAtualizado.pmSymbol   // => "PM"

// dias da semana baseado no `Locale`
calendarioUsuario.weekdaySymbols   // => ["Sunday", "Monday", "Tuesd…]
// nome dos meses baseado no `Locale`
calendarioUsuario.monthSymbols     // => ["January", "February", "Mar…]
// Note que temos também os prefixos `short` e `veryShort` caso precise de abreviações

// momento em que o dia se inicia
calendarioUsuario.startOfDay(for: Date())

// próximo final de semana a partir de uma data
calendarioUsuario.nextWeekend(startingAfter: Date())
```

## DateComponents
Uma das ferramentas mais poderosas do Foundation quando o assunto é trabalhar com datas. Isoladamente ela pode não parecer tudo isso -- apenas um container que trabalha com dias, meses, anos, etc. Em conjunto com o `Calendar`, eles nos fornecem recursos para realizarmos tarefas mais complexas, como cálculos utilizando datas ou mesmo criação de datas definindo os componentes.

`DateComponents` pode ser inicializada manualmente, e assume o valor `nil` caso não receba nenhum valor neste processo, porém ela é normalmente utilizada sendo extraída de uma data específica utilizando-se `Calendar`.
```swift
// Especificamos uma data e extraímos seus valores em componentes através de uma instância de Calendar
let agora = Date()
let componentes = calendarioUsuario.dateComponents([ .day, .month, .year ], from: agora)

componentes.year   // => 2017
componentes.month  // => 8
componentes.day    // => 29
```

> Observe que a função `dateComponents` de `Calendar` retorna um `Set` do tipo `Calendar.component`, que é basicamente uma instância de `DateComponent`. A lista completa de components possíveis você encontra [na documentação oficial.][doc-calendarcomponents]

## Criando Datas
Sim, é possível criar datas utilizando DateComponent de uma maneira mais legível -- e menos sofrida -- do que utilizando Date.
```swift
// Definimos os principais valores da data
var componentesAniversario = DateComponents()
componentesAniversario.year  = 1986
componentesAniversario.day   = 21
componentesAniversario.month = 8

// Usamos uma instância de Calendar para retornar um `Date` com a data definida.
calendarioUsuario.date(from: componentesAniversario)
// => "Aug 21, 1986, 12:00 AM"
```

## Calculando Datas
```swift
// Usamos um DateComponent definindo os valores a serem usados no calculo da data
var componentesCalculo = DateComponents()
componentesCalculo.day = 10
componentesCalculo.year = 1

// Utilizamos um calendário já instanciado para retornar a data utilizando o DateComponent definido
calendarioUsuario.date(byAdding: componentesCalculo, to: Date())
// 1 ano e 10 dias a partir da data determinada

// Outra forma de criar uma data, desta vez utilizando o `Calendar.Component`
calendarioUsuario.date(byAdding: .month, value: 1, to: Date())
// 1 mês a partir da data determinada
```

Trabalhar com datas pode não ser tão difícil quando entendemos como estas estruturas e classes se complementam dentro do Foundation. Associar os conceitos de [`Date`, `DateFormatter`][ninhoreference-date], `Calendar` e `DateComponent` fará com que você esteja preparado para lidar com quase todo tipo de operação utilizando datas.

Não deixe de ler a documentação oficial de [`Calendar`][doc-calendar] e [`DateComponents`][doc-datecomponents] para complementar ainda mais este conteúdo.

Até a próxima 🍻
\>}

[doc-calendar]: https://developer.apple.com/documentation/foundation/calendar
[doc-datecomponents]: https://developer.apple.com/documentation/foundation/datecomponents
[doc-calendaridentifier]: https://developer.apple.com/documentation/foundation/calendar.identifier
[doc-calendarcomponents]: https://developer.apple.com/documentation/foundation/calendar.component
[ninhoreference-enum]: https://ninhodaandorinha.com.br/posts/2017/8/8/enumeradores
[ninhoreference-date]: https://ninhodaandorinha.com.br/posts/2017/7/27/date-e-dateformatter
