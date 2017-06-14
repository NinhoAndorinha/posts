Swift 4: Controle de Acesso
===
Tivemos algumas mudanças em relação ao controle de acesso que podemos aplicar em nosso código. Vamos detalhar todos os níveis e o funcionamento de cada um para que você possa encontrar o que melhor se aplica ao seu caso.

Procure sempre de utilizar o nível adequado – mesmo que não esteja trabalhando em uma biblioteca – assim o compilador poderá fazer [alguns ajustes][dyndis] e melhorar a performance do seu código.

Funcionamento
---
Os níveis são baseados nos conceitos de **módulos** e **arquivos**.

Módulo é a unidade de distribuição – como bibliotecas ou aplicativos. São distribuídos como um único componente e podem ser importadas por outro módulo usando `import`. Note que cada _target_ no Xcode é tratado como um módulo separado.

Arquivo é um único arquivo com código Swift dentro de um módulo, ou seja, um arquivo dentro de uma aplicação ou biblioteca. Note que um único arquivo pode conter múltiplas definições de tipos, funções, etc.

Níveis
---
A Swift possui cinco níveis de acesso para serem utilizados. Esses níveis são relativos ao arquivo que a definição se encontra e também ao módulo que contém esse arquivo. Do menos restritivo ao mais restritivo, temos:

- **open**: Permite acesso à entidade – **incluindo** fazer [subclasse][subclass] ou [sobrescrita][override] – de qualquer arquivo do próprio módulo e de qualquer outro módulo que o importe. Recomendamos utilizar somente em definições que não tenham seu funcionamento alterado caso ocorra uma [subclasse][subclass] ou [sobrescrita][override];
- **public**: Permite acesso à entidade de qualquer arquivo do próprio módulo e de qualquer outro módulo que o importe. [Subclasses][subclass] e [sobrescrita][override] são permitidas somente no módulo onde foi feita a definição. É o nível de acesso comum para definições de interfaces públicas de uma biblioteca;
- **internal**: Restringe o acesso à entidade somente do módulo que ela foi definida. Tipicamente utilizada para definições internas do aplicativo ou biblioteca. É o nível padrão da Swift, portanto não é necessário explicitá-lo;
- **fileprivate**: Restringe o acesso à entidade somente ao arquivo que ela foi definida. Usado para esconder detalhes de implementação que são utilizados somente em um único arquivo, porém em múltiplas entidades. Na Swift 4 seu uso [será raro][fileprivate], sendo usada somente em casos onde realmente seja necessário a existência de múltiplas entidades em um arquivo;
- **private**: Restringe o acesso à entidade para a própria definição e extensões que estejam no mesmo arquivo. Usado para esconder detalhes de implementação que são utilizados somente pela própria definição da entidade;

Uso
---
Os níveis de acesso seguem o seguinte princípio: Nenhuma entidade pode ter um nível menos restritivo que a definição que a contém. Por exemplo:

- uma propriedade marcada como `public` não pode ser de um tipo marcado como `private`;
- um método marcado como `open` não pode existir em uma classe marcada como `internal`;

Lembre que os níveis são relativos aos arquivos e módulos, então sempre temos que seguir a ordem: `open > public > internal > fileprivate > private`. O nível de acesso padrão é `internal` mas pode ser alterado quando usamos em uma entidade que tenha um nível menor. Por exemplo:
```swift
class ClasseInterna {         // implicitamente internal
	func metodoInterno() {}   // implicitamente internal
}
```
```swift
private class ClassePrivada {   // explicitamente private
	func metodoInterno() {}     // implicitamente private
}
```
Note que esse efeito só ocorre em níveis mais restritivos que `internal`:
```swift
public class ClassePublica {   // explicitamente public
	func metodoInterno() {}    // implicitamente internal
}
```

Recomendações
---
No geral em classes e estruturas deixe `internal`, nos membros procure usar `private` – assim você irá ganhar as [otimizações do compilador][dyndis] – e caso seja necessário vá aumentando o nível gradativamente.

Caso esteja escrevendo uma biblioteca prefira `public` na sua interface, a menos que tenha certeza que a entidade possa sofrer [subclasse][subclass] ou [sobrescrita][override] sem alteração no funcionamento.

Com isso em mente, não deixe de ajustar os níveis de acesso de acordo com a necessidade de seu código.

Até a próxima!
\>}

[dyndis]: https://developer.apple.com/swift/blog/?id=27
[subclass]: https://pt.wikipedia.org/wiki/Herança_(programação)
[override]: https://pt.wikipedia.org/wiki/Redefinição_de_métodos
[fileprivate]: https://github.com/apple/swift-evolution/blob/master/proposals/0169-improve-interaction-between-private-declarations-and-extensions.md
