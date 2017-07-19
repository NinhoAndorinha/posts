# Gerenciador de Pacotes: Homebrew
No dia-a-dia de um desenvolvedor, é comum utilizar [pacotes][wiki-pkg] para realizar seu trabalho. Seja uma ferramenta como `git` ou um interpretador como `node`, o processo de instalação pode ser bem trabalhoso.

Por isso é comum a utilização de algum [Gerenciador de Pacotes][wiki-pm] -- como nos sistemas [GNU/Linux][linux]. A Apple não disponibilizou um oficialmente 😢, mas felizmente a comunidade de usuários criou o [Homebrew][link-brew]🍻.

Com ele é possível buscar, instalar, atualizar, apagar, etc. Tudo de maneira simples e automatizada.

## Instalando o Homebrew
Para instalar vamos utilizar a linha de comando, busque por **Terminal** no _Spotlight_ ou pelo _Finder_ em:
`Applications > Utilities > Terminal.app`

![Terminal.app][01-terminal]

Após aberto basta colar o seguinte comando e pressionar _enter_:
```sh
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

Pronto! O processo de instalação é guiado e bem rápido.

## Pacotes
Agora que temos o [Homebrew][link-brew] instalado podemos usá-lo para gerenciar pacotes. Vamos começar com a **busca**. Caso queira achar todos os pacotes disponíveis relacionados a `git` basta usar o comando `brew search <termo>`, por exemplo:
```sh
brew search git
```

Quando encontrar o pacote que deseja instalar, usamos `brew install <nome do pacote>`:
```sh
brew install git
```

Para atualizar o pacote temos o comando `brew upgrade <nome do pacote>`:
```sh
brew upgrade git
# ou podemos atualizar todos com:
brew upgrade
```

E caso não esteja mais utilizando algum pacote e quiser remove-lo, pode utilizar `brew uninstall`:
```sh
brew uninstall git
```

## Atualizando o Homebrew
A comunidade está sempre criando novos pacotes e os atualizando para as versões mais recentes. Para manter seu _brew_ atualizado recomendamos executar `brew update` pelo menos uma vez por semana. Lembre-se que essa frequência só é importante se você utiliza os pacotes diariamente. Após atulizar o _brew_ é possível listar todos os pacotes que estão desatualizados com `brew outdated`.
```sh
# atualiza o brew
brew update

# lista os pacotes desatualizados
brew outdated

# atualiza todos os pacotes e limpa as versões antigas
brew upgrade --cleanup
```

## O que instalar?
Segue uma lista de alguns pacotes que consideramos úteis
```sh
# Controle de Versão:
brew install git
brew install mercurial

# Manipulação de Arquivos
brew install ack  # busca de texto
rename            # renomeia de acordo com regras ou regex

# Linguagens
brew install node
brew install python
brew install ruby
brew install swiftenv  # instala versões de desenvolvimento da Swift :)

# Rede
nmap
wireshark
wget
youtube-dl  # download de videos
```

Não se esqueça de ver a [documentação completa][doc-brew] para saber todas as possibilidades do _brew_.

Até a próxima! 🍻
\>}

[link-brew]: https://brew.sh
[doc-brew]: http://docs.brew.sh/
[linux]: https://pt.wikipedia.org/wiki/GNU/Linux
[wiki-pkg]: https://pt.wikipedia.org/wiki/Pacote_de_software
[wiki-pm]: https://pt.wikipedia.org/wiki/Sistema_gestor_de_pacotes

[01-terminal]: /_img/talk-is-cheap/2017-07-08-gerenciador-de-pacotes-homebrew/01-terminal.png
