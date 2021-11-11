# _Derivações_

_Derivação_ é o conceito de funções puras aplicadas a arquivos. A forma tradicional é utilizando a memória RAM.

Linguagens de programação geralmente usam um espaço de memória alocado dinamicamente para guardar os objetos em blocos, nas _derivações_ o espaço alocado é na _nix-store_, que geralmente se localiza na pasta `/nix/store`. Cada objeto é um item nessa pasta.

Os itens dessa pasta podem ser classificados em dois tipos:
- _Derivações_: aqueles arquivos de extensão `drv` que são basicamente especificações mastigadas para realizar as transformações.
em uma derivação
- _Closures_: outros arquivos e pastas, o produto final.

O processo de transformar uma derivação em uma closure é chamado de _realization_, esses caminhos são gerados
dos `drv` ou baixados de caches se disponível.

As _closures_ podem ser apenas um arquivo ou uma pasta com arquivos.

_Derivações_ podem ter dependências em outras _derivações_, o que gera um efeito cascata. Se `a` depende de `b` e `a` for realizada primeiro o Nix realizará `b` e então realizará `a`. Este conceito de dependência é aplicado para substituir o [comportamento de _hashmap_](analogia-hashmap-arvore.md) de gerenciadores de pacote tradicionais e permite que o Nix tenha dois pacotes do mesmo programa em versões diferentes sem que um conflite com o outro, assim como uma árvore.

O resto basicamente aproveita esta base para produzir algo mais complexo, inclusive o NixOS, sistemas de módulos, scripts de ativação e tudo mais.
