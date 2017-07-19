# Acessibilidade
Cada vez mais a Apple vem trabalhando em tecnologias para deixar seus produtos acessíveis a todos. Infelizmente poucos desenvolvedores incluem esses recursos em seus apps.

Queremos mudar esse cenário! Após esse tutorial você vai ver o quão simples é implementar o básico de acessibilidade no seu aplicativo, e com isso incluir milhares de novos usuários.

## Por que?
De acordo com a [Organização Mundial da Saúde][who] temos mais de um bilhão de pessoas com deficiência no mundo -- 1 em cada 7 -- portanto provavelmente você já tem usuários que agradeceriam se seu aplicativo tivesse acessibilidade e outros que ainda não conseguem usá-lo.

As `API`s de acessibilidade estão presentes em todas as plataformas da Apple, vamos exemplificar aqui com o iOS por ser o maior foco de desenvolvimento atualmente.

---

## Dynamic Type
Introduzido no iOS7 o _Dynamic Type_ -- ou _Texto Maior_ -- é um sistema que permite aos usuários ajustar dinamicamente o tamanho do texto. Por padrão possui **sete** configurações de tamanho e mais **cinco** quando ativada a opção de acessibilidade.

`Ajustes > Geral > Acessibilidade > Texto Maior`

![Dynamic Type no iOS][01-dyntype-ios]

Para implementar o _Dynamic Type_ precisamos ajustar a fonte do texto para um dos [estilos de texto][doc-fontstyles] e habilitar a propriedade [`adjustsFontForContentSizeCategory`][doc-fontadjust]. No Xcode 9 tudo isso pode ser feito pelo storyboard:

![Dynamic Type no Xcode 9][02-dyntype-xcode]

Ou via código:
```swift
label.font = UIFont.preferredFont(forTextStyle: .body)
label.adjustsFontForContentSizeCategory = true
```

Temos os seguintes estilos para a visualização padrão e aumentada (Fonte Tamanho):

![Estilos de texto][03-fontstyles]

#### Fontes Customizadas
Caso seu aplicativo utilize uma fonte customizada não se preocupe, no iOS 11 ficou fácil de aplicar o _Dynamic Type_ a qualquer fonte usando o [`UIFontMetrics`][doc-fontmetrics]. Podemos escalar nossas fontes customizadas de acordo com a métrica _default_, que representa o estilo _.body_.
```swift
label.font = UIFontMetrics.default.scaledFont(for: fonteCustomizada)
```

Recomendamos definir as fontes de acordo com os estilos, assim as variações serão proporcionais. Lembre-se que mesmo que seja utilizada a mesma fonte para todos os textos, os tamanhos e atributos podem variar, por isso devemos definir os estilos separadamente e deixar o `UIFontMetrics` acertar a proporção.
```swift
labelTitulo.font = UIFontMetrics(forTextStyle: .title1).scaledFont(for: fonteCustomizadaTitulo)
labelConteudo.font = UIFontMetrics(forTextStyle: .body).scaledFont(for: fonteCustomizadaConteudo)
```

![Estilos de texto em fonte customizada][04-fontstyles-custom]

---

## VoiceOver
Agora que já ajustamos o tamanho de nossos textos dinamicamente, vamos implementar o _VoiceOver_. Essa funcionalidade lê os itens da tela em voz alta.

O processo é bem simples, seu funcionamento consiste em fazer os elementos responderem a três perguntas: Qual função? Qual título? Qual valor? Essas perguntas equivalem às propriedades `accessibilityTraits`, `accessibilityLabel` e `accessibilityValue` respectivamente.

Imagine que a tela que deixaremos acessível tem dois _botões_ e uma _label_. Um _botão_ zera o valor da _label_ e o outro incrementa seu valor:

![Exemplo de tela com VoiceOver][05-voiceover-sample-app]

Começamos adicionando algumas propriedades pelo storyboard:

![Acessibilidade no Xcode 9][06-xcode-accessibility]

Repare que além das três propriedades que comentamos anteriormente, o Xcode exibe outras duas, totalizando os cinco atributos do [`UIAccessibilityElement`][doc-accelement]. Com isso temos:
- **isAccessibilityElement**: se o elemento deve ser marcado como acessível -- por padrão todos os controles do `UIKit` são;
- **accessibilityLabel**: nome do elemento de forma sucinta, preferencialmente localizado;
- **accessibilityTraits**: aspecto do comportamento, estado ou uso do elemento. Múltiplos aspectos podem ser combinados;
- **accessibilityHint**: descrição resumida do resultado da ação ou conteúdo do elemento -- preferencialmente localizada;
- **accessibilityValue**: valor atual do elemento, um _slider_ pode ter valor _"42%"_ por exemplo;

Para completar nosso exemplo, precisamos atribuir um _valor_ na _label_ quando carregar a tela e toda vez que o valor do contador for alterado, vamos ao código:
```swift
labelDisplay.accessibilityValue = "Valor atual: \(contador.valor)"
```

Com isso, ao rodar o aplicativo no iPhone e ligar o _VoiceOver_, vemos que os elementos são selecionados sequencialmente e tem seus nomes falados em voz alta. Ao testar nesse modo podemos reparar que seria muito mais vantajoso se os botões também tivessem seus _valores_ atribuídos junto com a _label_. Portanto ao atualizar o valor do contador temos agora:
```swift
let valor = "Valor atual: \(contador.valor)"
labelDisplay.accessibilityValue = valor
buttonZerar.accessibilityValue  = valor
buttonContar.accessibilityValue = valor
```

## Inspetor de Acessibilidade
Como você já deve saber, nada substitui o teste no aparelho, porém as vezes podemos ganhar tempo usando simuladores ou inspetores. O Xcode tem uma ferramenta inspecionar a acessibilidade do seu aplicativo -- o _Accessibility Inspector_. Nele é possível testar opções como tamanhos do _Dynamic Type_, cores invertidas, etc. sem precisar alterar os valores no _Ajustes_. Também é possível realizar uma auditoria onde são encontrados problemas comuns, e inclusive soluções são sugeridas.

![Inspetor de Acessibilidade][07-inspector]

## E agora?
Esperamos que essa pequena introdução o incentive a incluir acessibilidade nos seus projetos, além de ganhar usuários você estará contribuindo para um mundo cada vez mais acessível. Reserve alguns minutos para assistir a [melhor palestra][cyim] da **#WWDC17** -- [Conveniência para você é Independência para mim][cyim] do [Todd Stabelfeldt][quadfather].

Outras palestras importantes são: [Design para Todos][dfe], [Novidades em Acessibilidade][whatsnew] e [Auditando a Acessibilidade de seus apps][inspector]. Não deixe de conferir a [documentação oficial][doc-accessibility] e experimentar o _Accessibility Inspector_ em seus aplicativos.

Até a próxima!
\>}

[who]: http://www.who.int/disabilities/en/
[doc-fontadjust]: https://developer.apple.com/documentation/uikit/uicontentsizecategoryadjusting/1771731-adjustsfontforcontentsizecategor
[doc-fontstyles]: https://developer.apple.com/documentation/uikit/uifonttextstyle
[doc-fontmetrics]: https://developer.apple.com/documentation/uikit/uifontmetrics
[doc-accelement]: https://developer.apple.com/documentation/uikit/uiaccessibilityelement
[cyim]: https://developer.apple.com/videos/play/wwdc2017/110/
[quadfather]: https://www.facebook.com/ToddStabelfeldt
[dfe]: https://developer.apple.com/videos/play/wwdc2017/806/
[whatsnew]: https://developer.apple.com/videos/play/wwdc2017/215/
[inspector]: https://developer.apple.com/videos/play/wwdc2016/407/
[doc-accessibility]: https://developer.apple.com/accessibility/

[01-dyntype-ios]: /img/tutoriais/2017/06/23/acessibilidade/01-dyntype-ios.png
[02-dyntype-xcode]: /img/tutoriais/2017/06/23/acessibilidade/02-dyntype-xcode.png
[03-fontstyles]: /img/tutoriais/2017/06/23/acessibilidade/03-fontstyles.png
[04-fontstyles-custom]: /img/tutoriais/2017/06/23/acessibilidade/04-fontstyles-custom.png
[05-voiceover-sample-app]: /img/tutoriais/2017/06/23/acessibilidade/05-voiceover-sample-app.png
[06-xcode-accessibility]: /img/tutoriais/2017/06/23/acessibilidade/06-xcode-accessibility.png
[07-inspector]: /img/tutoriais/2017/06/23/acessibilidade/07-inspector.png
