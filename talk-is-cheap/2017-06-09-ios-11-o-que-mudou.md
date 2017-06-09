iOS 11: O que mudou?
===
A **#WWDC17** chegou ao fim 😔 e a essa altura você já deve ter visto todas as novidades do iOS 11, mas talvez esteja se perguntando: o que mudou para os desenvolvedores?

Peraí! Não viu as novidades? Não tem problema, dê uma olhadinha [nesse post][bdi-ios] do Blog do iPhone que tem uma lista bem bacana.

Abaixo separamos algumas funcionalidades bem interessante para começar a explorar o iOS 11. Para uma lista completa de mudanças não deixe de ver a [documentação oficial][api-diff].

Arrastar e Soltar
---
Nessa versão o **iPad** ganhou uma função muito bem vinda: Arrastar e Soltar, com isso a produtividade dos usuários irá melhorar muito. Com poucas linhas de código podemos implementar essa função no nosso aplicativo.

O suporte ao Arrastar e Soltar são nativos para os seguinte elementos: `TableView`, `CollectionView`, `TextView`, `TextField`, `WebView` e também estão integrados ao `UIPasteConfiguration`. Tornando a adoção dessa função muito fácil.

NFC
---
No **iPhone 7 e 7 Plus** -- e provavelmente aparelhos futuros -- o novo sistema operacional vai permitir que os desenvolvedores tenham acesso ao NFC. Agora será possível usar o `CoreNFC` para ler tags dos tipos 1 à 5 em NFC Data Exchange Format (NDEF). O código é bem simples, mas o processo é tedioso e envolve:
- Criação manual de `App ID` e `Provisioning Profile` no [portal de desenvolvedores][apple-dev];
- Configuração manual dos `Entitlements` na aplicação;
- Ajustes no `Info.plist`;

Passado todo esse transtorno, o processo de leitura é bem simples, bastando:
- Importar o framework `CoreNFC`;
- Criar uma instância do leitor;
- Começar a escanear;
- Receber as informações via _delegate_;

Manipulação de Arquivos
---
Além do novo aplicativo nativo _Files_, estão disponíveis novas APIs para a manipulação de arquivos. Podemos acessar um visualizador de arquivos (locais e nuvem) através do `UIDocumentBrowserViewController` e de forma altamente customizável.

Lembre-se de coordenar o acesso aos arquivos utilizando `NSFileCoordinator` ou `UIDocument`.

Nova Barra de Navegação
---
Tivemos uma prévia dessa novidade com o aplicativo _Música_ ainda no iOS 10, agora a barra de navegação ficou um pouco maior para poder abrigar o título em letras maiores e uma barra de busca. Porém a barra diminui quando a tela é movida para cima, ganhando mais espaço para exibir o conteúdo.

A implementação não é automática, porém é bem simples, temos duas propriedades a serem ajustadas. Uma faz com que o título fique no tamanho grande e outra altera o modo de exibição durante a navegação.

A sugestão da Apple é que a primeira tela da navegação seja com título grande e todas as seguintes não. Esse já é o comportamento padrão quando a funcionalidade é adotada.

Área Segura
---
Como a nova barra de navegação pode variar a altura, agora temos uma maneira bem simples de ajustar o conteúdo de acordo com o tamanho dela -- caso seja necessário já que os componentes padrões fazem isso automaticamente.

Usando a propriedade `.top` do `safeAreaInsets` temos o valor atualizado da altura da barra. Também exite a propriedade `.bottom` que nos retorna a altura da barra inferior (caso exista, ex: `UITabBar`).

Além dos _insets_ podemos usar a área segura como âncora do AutoLayout através do `safeAreaLayoutGuide` e com isso automatizar o processo de ajuste do conteúdo de acordo com as variações da área.

O `UIScrollView` agora se ajusta sozinho usando a área segura e não mais o `contentInset`, deixando ele livre para ser manipulado por nós.

Ações ao Deslizar
---
Podemos incluir ações de célula do `UITableView` no lado direito e esquerdo e ações padrão para serem executadas quando a célula for deslizada até o final.

Só tome cuidado para essa não ser a única maneira de se realizar a ação, pois dessa forma elas estão escondidas do usuário.

Arquivando Tipos Nativos
---
O _Swift 4_ e o _Foundation_ fizeram uma aproximação muito importante nessa atualização, o protocolo `Codable` foi introduzido, nos possibilitando codificar tipos nativos da Swift usando `NSCoding`, `JSON` e `Plist`. Com isso, podemos decodificar `JSON` diretamente para nosso objeto modelo.

KVO
---
Para os amantes do [Key-Value Observing][doc-kvo] ele chegou na Swift, e melhor ainda, usando _closures_ ❤️. Também foi introduzida uma forma de declarar os _keypath_ de forma literal, deixando seu uso muito mais prático e seguro.

Preenchimento de Senhas
---
Agora o iOS detecta se o aplicativo tem uma tela de acesso com nome de usuário e senha, e exibe um campo de preenchimento com as senhas do iCloud.

Por padrão será exibida uma lista com todas as senha e um campo de busca, para melhorar esse processo, devemos fazer uma alteração no `Entitlements` e adicionar um `JSON` no servidor. Essas etapas são basicamente as mesmas da implementação dos Links Universais.

Tem mais?
---
Muito mais! Diversas outras funcionalidades e melhorias foram feitas nessa atualização, como eles mesmo disseram o foco foi produtividade, refinamentos e melhorias.

Além de tudo que detalhamos, algumas outras merecem ser citadas:
- Assets Catalog
	- Podemos adicionar cores (inclusive _wide gamut_);
	- O ícone agora participa do _App Thinning_;
	- As imagens em PDF podem manter os dados vetoriais e serem redimensionadas de acordo com o `Dynamic Type` selecionado;
- AutoLayout
	- Agora o `UIScrollView` usa dois sistemas de âncora, um externo e outro interno, simplificando muito a centralização no zoom;
	- Espaçamento entre `UILabel`s recomendado pelo sistema usando âncoras de _baseline_ com `Dynamic Type`;
- Dynamic Type
	- Ajuste das fontes customizadas através do `UIFontMetrics` que calcula o tamanho proporcional ao padrão do sistema;
	- Ajustar tamanhos arbitrários mantendo a proporção correta com `UIFontMetrics` (ex: altura de um `UIButton`);

Nas próximas semanas iremos detalhar diversas dessas funcionalidades com exemplos e muito código, não perca!

Até a próxima!
\>}

[bdi-ios]: https://blogdoiphone.com/2017/06/confira-algumas-novidades-que-virao-no-ios-11/
[api-diff]: https://developer.apple.com/documentation?changes=latest_minor
[apple-dev]: https://developer.apple.com/
[doc-kvo]: https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/KeyValueObserving/KeyValueObserving.html
