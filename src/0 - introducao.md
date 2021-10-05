# Introdução

Nix é uma ferramenta que aplica conceitos e questões da programação funcional em transformação de arquivos.
Um dos títulos que dão ao Nix é que ele é um gerenciador de pacotes mas a base dele permite que ele seja mais.

O Nix em sí é uma linguagem de programação de tipagem dinâmica que segue o paradigma funcional e seus conceitos mas que possui um diferencial que
muda totalmente o jogo: O conceito de _derivation_.

# O que são _derivations_?

Derivations são o conceito de funções puras aplicado a arquivos. Enquanto que em outras linguagens, e no Nix também, os objetos
manipulados por estas linguagens estão guardados na memória RAM para processamento o Nix tem como operar com transformações
em arquivos.

Linguagens de programação geralmente usam um espaço de heap em que alocam memória para os objetos em blocos, nas _derivations_ o espaço alocado é na _nix-store_, que geralmente se localiza na pasta `/nix/store`. Cada objeto é um item nessa pasta.

Os itens dessa pasta podem ser classificados em dois tipos:
- _Derivations_: aqueles arquivos de extensão `drv` que são basicamente especificações mastigadas para realizar as transformações 
em uma _derivation_
- _Realizations_: o processo de transformar uma definição no objeto em sí é chamado de realization, esses caminhos são gerados
dos `drv` ou baixados de caches.

As realizations podem então ser apenas um arquivo ou uma pasta com arquivos.

Derivations podem ter dependências em outras _derivations_ o que gera um efeito cascata. Se `a` depende de `b` se `a` for realizada primeiro o Nix vai realizar a `b` e então realizar a `a`. Esse conceito de dependência é aplicado para substituir o comportamento de hashmap de gerenciadores de pacote tradicionais e permite que o Nix tenha dois pacotes do mesmo programa em versões diferentes sem que um conflite com o outro tendo então um comportamento de árvore. Essa analogia será melhor explicada em breve.

O resto basicamente aproveita essa base para produzir algo mais complexo, inclusive o NixOS, sistemas de módulos, scripts de ativação e tudo mais.
