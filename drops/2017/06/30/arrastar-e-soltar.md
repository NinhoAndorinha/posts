# Drag & Drop
Vamos dar uma olhada rápida no funcionamento do _Drag & Drop_ -- Arrastar e Soltar.
Essa _API_ é bem interessante e completa, por isso não deixe de conferir a [documentação oficial][doc-dragndrop] para todos os detalhes de seu funcionamento e [essa palestra][link-wwdc] da **#WWDC17**.

## Drag
Para habilitar a interação de arrastar -- em inglês *drag* -- basta criar um `UIDragInteraction` e adicioná-lo a _view_ que desejamos arrastar. Repare que o procedimento é similar ao [UIGestureRecognizer][doc-gesture].
```swift
let drag = UIDragInteraction(delegate: self)
view.addInteraction(drag)
```

Na criação da interação atribuímos um delegate para receber os eventos, portanto temos que conformar com o protocolo [`UIDragInteractionDelegate`][doc-dragdelegate]. O único método exigido é [`dragInteraction(_, itemsForBeginning:)`][doc-dragdelegate-method], nele devemos retornar o item que está sendo arrastado.
```swift
func dragInteraction(_ interaction: UIDragInteraction, itemsForBeginning session: UIDragSession) -> [UIDragItem] {
    // Para passar o modelo do item arrastado usamos um `NSItemProvider`,
    // como a API pede um objeto, vamos transformar a estrutura String da Swift
    // em NSString do Foundation
    let item = NSItemProvider(object: "Arrastando" as NSString)

    // Note que retornamos um array pois um _drag_ pode conter múltiplos objetos
    return [ UIDragItem(itemProvider: item) ]
}
```

## Drop
Na interação de soltar -- em inglês _drop_ -- o procedimento é o mesmo, criamos um `UIDropInteraction` e o adicionamos na _view_ que receberá o item.
```swift
let drop = UIDropInteraction(delegate: self)containerView.addInteraction(drop)
```

No delegate [`UIDropInteractionDelegate`][doc-dropdelegate] temos o processamento do item a ser recebido. Primeiro vamos ajustar a operação a ser executada quando recebermos um _drop_, essa configuração altera o ícone que será exibido quando o item for arrastado em cima do alvo do _drop_.
```swift
func dropInteraction(_ interaction: UIDropInteraction, sessionDidUpdate session: UIDropSession) -> UIDropProposal {
    // Temos algumas opções (em ordem de mais utilizada para menos):
    //   - .cancel: cancela o _drag_, não tranfere nenhuma informação;
    //   - .copy: aceita o _drag_, as informações dos itens devem ser copiadas;
    //   - .move: aceita o _drag_, as informações devem ser movidas;
    //   - .forbidden: não aceita o _drag_, apesar de normalmente esse alvo
    //                 aceitar um _drag_, no momento não está aceitando;
    return UIDropProposal(operation: .copy)
}
```

Agora vamos processar o _drop_. Como o item (ou itens) de origem pode demorar para chegar -- pode ser um arquivo grande ou até um download -- essa operação é executada em segundo plano.
```swift
func dropInteraction(_ interaction: UIDropInteraction, performDrop session: UIDropSession) {
    // Usamos o método `loadObjects` para carregar os itens, assim que estiverem
    // disponíveis a _closure_ será executada. Como nosso exemplo de _drag_
    // passamos uma `NSString`, estamos especificando aqui.
    session.loadObjects(ofClass: NSString.self) { itens in
        // Vamos transformar a `NSString` em `String` e percorrer
        // todos os itens -- caso existam.
        for item in itens as! [String] {
          print(item)
        }
    }
}
```

## Exemplo
Preparamos um exemplo completo para você testar.
Crie um projeto iOS e no storyboard adicione uma `UILabel` e um `UITextView`. **NÃO se esqueça** de habilitar a propriedade `User Interaction Enabled` da _label_ -- para poder receber o toque -- **e** utilizar o simulador do **iPad**.
```swift
class ViewController: UIViewController {
    @IBOutlet weak var label: UILabel!
    @IBOutlet weak var textView: UITextView!

    override func viewDidLoad() {
        super.viewDidLoad()

        let drag = UIDragInteraction(delegate: self)
        label.addInteraction(drag)

        let drop = UIDropInteraction(delegate: self)
        textView.addInteraction(drop)
    }
}

extension ViewController: UIDragInteractionDelegate {
    func dragInteraction(_ interaction: UIDragInteraction, itemsForBeginning session: UIDragSession) -> [UIDragItem] {
        let item = NSItemProvider(object: "Arrastando" as NSString)
        return [ UIDragItem(itemProvider: item) ]
    }
}

extension ViewController: UIDropInteractionDelegate {
    func dropInteraction(_ interaction: UIDropInteraction, sessionDidUpdate session: UIDropSession) -> UIDropProposal {
        return UIDropProposal(operation: .copy)
    }

    func dropInteraction(_ interaction: UIDropInteraction, performDrop session: UIDropSession) {
        session.loadObjects(ofClass: NSString.self) { itens in
            for item in itens as! [String] {
                let texto = self.textView.text + "\n\(item)"
                self.textView.text = texto
            }
        }
    }
}
```

Veja o projeto completo no [GitHub][github].

Até a próxima!
\>}

[doc-dragndrop]: https://developer.apple.com/documentation/uikit/drag_and_drop
[link-wwdc]: https://developer.apple.com/videos/play/wwdc2017/203/
[doc-gesture]: https://developer.apple.com/documentation/uikit/uigesturerecognizer
[doc-dragdelegate]: https://developer.apple.com/documentation/uikit/uidraginteractiondelegate
[doc-dragdelegate-method]: https://developer.apple.com/documentation/uikit/uidraginteractiondelegate/2891010-draginteraction
[doc-dropdelegate]: https://developer.apple.com/documentation/uikit/uidropinteractiondelegate
[github]: https://github.com/NinhoAndorinha/ArrastaSolta
