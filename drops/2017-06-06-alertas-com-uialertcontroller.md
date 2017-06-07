Alertas com UIAlertController
===
Existem diversas formas de alertar o usuário em um aplicativo iOS. Seja para comunicar um acontecimento, exibir um erro, obter uma informação ou decisão, etc. Muitas vezes a melhor -- e mais simples -- é utilizando o `UIAlertController`.

O `UIAlertController` herda de `UIViewController` e **não** foi projetado para ser usado como subclasse, por isso sempre o utilize diretamente. Seu objetivo é exibir uma mensagem de alerta e dar ao usuário uma maneira de respondê-la. Está disponível a partir do iOS 8, onde veio para substituir o `UIAlertView` e o `UIActionSheet`, que ficaram obsoletos a partir desta versão.

Criando um alerta
---
Um alerta é composto por:
- **Title**: Título utilizado para chamar a atenção e comunicar a razão do alerta.
- **Message**: um texto descritivo do que aconteceu.   
- **Style**: maneira a ser exibida[^fn-alert-style].

```swift
let alerta = UIAlertController(
                title: "Falha de Comunicação",
                message: "Houve um erro durante a comunicação com nosso servidor, por favor tente novamente mais tarde.",
                preferredStyle: .alert)
// Note que em preferredStyle podemos simplificar UIAlertControllerStyle.alert
// por .alert por causa da inferência de tipos da Swift.
```

Configurando ações
---
As ações são a forma do usuário responder ao alerta e contém:
- **Title**: Título a ser exibido no botão.
- **Style**: estilização do botão[^fn-action-style].
- **Handler**: código que será executado ao selecionar o botão.

```swift
let ok = UIAlertAction(title: "Ok", style: .cancel, handler: nil)
// Note que nesse caso estamos passando nil no handler pois não queremos
// executar nada quando o usuário selecionar esse botão.
```

Adicionando ações
---
Depois de criadas temos que adicioná-las ao botão. Se um alerta tiver múltiplas ações, elas serão exibidas na ordem que foram adicionadas.
```swift
alerta.addAction(ok)
```

Exibindo
---
Depois de configurado, basta exibir o alerta através do método: [`present(_:animated:completion:)`][doc-present] do `UIViewController`. Aqui podemos escolher se irá ocorrer animação ou ainda executar alguma ação depois de exibir.
```swift
present(alerta, animated: true, completion: nil)
// Escolhemos a exibição animadamente - animated: true
// e nenhuma ação depois de exibir - completion: nil
```

Exemplo completo
---
```swift
// criação
let alerta = UIAlertController(
    title: "Falha de Comunicação",
    message: "Houve um erro durante a comunicação com nosso servidor, por favor tente novamente mais tarde.",
    preferredStyle: .alert)
// ações
let ok = UIAlertAction(title: "Ok", style: .cancel, handler: nil)
alerta.addAction(ok)
// exibindo
present(alerta, animated: true, completion: nil)
```

Não deixe de consultar sempre a [documentação oficial][doc-alert] para ver todas as propriedades e métodos e explorar ainda mais possibilidades do `UIAlertController`.

Até a próxima!
\>}

[doc-present]: https://developer.apple.com/documentation/uikit/uiviewcontroller/1621380-present
[doc-alert]: https://developer.apple.com/documentation/uikit/uialertcontroller

[^fn-alert-style]: Podemos utilizar **.alert**, mostrando um balão no centro da tela ou **.actionSheet**, mostra um bloco de ações vinda da parte inferior da tela.
[^fn-action-style]: Temos o estilo padrão **.default**, **.cancel** onde segue o estilo dos botões cancelar do iOS e **.destructive** onde o iOS sinaliza ao usuário que a ação será destrutiva.
