# Xcode 9: Finalmente
A mais nova versão do Xcode foi completamente repensada com foco em produtividade e velocidade. Trazendo diversas novidades e realizando diversos desejos pedidos pelos desenvolvedores há anos.

Esse foi o mais importante anúncio da WWDC já que afeta desenvolvedores de todas as plataformas. Pela quantidade de funcionalidades -- há muito requisitadas -- que foram entregues, carinhosamente apelidamos essa versão de: *Xcode Finalmente*.

A seguir você encontrará a lista das mudanças que mais gostamos por enquanto, mas não deixe de conferir todas as novidades no [site da Apple][rn-xcode9].

## Editor
Nessa atualização o editor foi completamente re-escrito em Swift ❤️. A diferença é perceptível ao navegar pelos arquivos, não importando a quantidade de linhas ou tamanho, a resposta é imediata. Nota-se uma sensação de prontidão e responsividade jamais vista.

Agora podemos ajustar diversos aspectos do editor como estilos de fonte, espaçamento entre as linhas e até mesmo o tipo de cursor. A novidade mais bem-vinda foi poder controlar o tamanho da fonte usando o atalho: <kbd>&#8984;</kbd>+<kbd>+</kbd> e <kbd>&#8984;</kbd>+<kbd>-</kbd>.

Tivemos também a inclusão da formatação de textos usando [Markdown][df-md]. Nos arquivos com esse tipo de marcação o editor automaticamente aplica o visual adequado aos cabeçalhos, negritos, itálicos, links, etc. no momento da digitação.

## Issues
A maneira de exibir os alertas de problemas (warnings e errors) foi redesenhada e os pop-ups de fix-it também estão mais fáceis de utilizar, podendo inclusive realizar múltiplas alterações simultaneamente. Uma ótima adição de fix-it foi o auto-preenchimento dos requisitos dos protocolos conformados 🙏.

## Refatoração
Outra área que o Xcode estava devendo (e muito) era refatoração de código. Agora embutida no editor estão os motores de refatoração e transformação. Podendo executar operações poderosas em questão de segundos e sem sair do editor. Algumas das diversas operações possíveis são:
- Renomear no projeto (incluindo Storyboards 🎉)
- Extração de variáveis locais
- Extração de métodos/expressões
- Expansão de `switch-case`
- Conversão de `if-else` para `switch-case` e vice versa
- Transformação de `String` em `NSLocalizedString`

Todas as transformações funcionam em Swift, Objective-C, C e C++ e funcionam inclusive entre os arquivos de diferentes linguagem. Além da barra de menu, podemos acessá-las através de um click durante a visualização de estruturas -- que foi importada do Swift Playgrounds -- segurando a tecla <kbd>&#8984;</kbd>. Esses motores de refatoração e transformações terão seu código fonte publicado junto com o projeto do compilador `Clang`.

## Geral
Como se ainda não bastasse as melhorias na edição, também tivemos diversas funcionalidades adicionadas nas funções que complementam o desenvolvimento. Agora podemos cortar o cabo e instalar nos aparelhos através de uma conexão sem fio.

Temos um novo sistema de `build`, que por enquanto tem que ser habilitado manualmente, que promete ser bem mais rápido que o atual e que acontece em paralelo com a indexação 🍻.

Podemos lançar simultaneamente diversos simuladores para agilizar inclusive o processo de testes automatizados. Os novos simuladores incluem um bisel[^fn-bisel] com botões funcionais e de onde podemos testar gestos que começam de fora da tela.

Em uma parceria com o GitHub teremos agora uma integração bem mais profunda, podendo realizar todas as tarefas pelo próprio Xcode. Do lado do GitHub, teremos um botão que irá clonar o projeto e abrir direto no Xcode.

Se tivermos que resumir o as atualizações dessa versão em uma palavra seria *produtividade*. Parece que a Apple realizou praticamente todos os pedidos de todos os desenvolvedores dos últimos anos, esperamos que as melhorias e inovações continuem pois sempre existirá algo a melhorar 🚀.

Até a próxima!
\>}

[rn-xcode9]: https://developer.apple.com/library/content/documentation/DeveloperTools/Conceptual/WhatsNewXcode/xcode_9/xcode_9.html
[df-md]: https://daringfireball.net/projects/markdown/

[^fn-bisel]: O anel em torno do mostrador de um relógio que, tipicamente, mantém o vidro ou cristal que cobre o mostrador no lugar. A borda do iPhone/iPad também é conhecida assim.
