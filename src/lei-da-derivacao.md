# Lei da `Derivação`

Seja
- uma derivação D(a, b, c, ...) = z que transforma as entradas em z.
- uma [função de hash](https://pt.wikipedia.org/wiki/Fun%C3%A7%C3%A3o_hash) H(x) que calcula um hash de algum x, pode ser por exemplo a [SHA256](https://pt.wikipedia.org/wiki/SHA-2).

Uma `realização` de uma `derivação` precisa:

- Para ter acesso a internet: H(z) pré-definido
- Para conseguir executar sem H(z) definido: a definição de todas as derivações de entrada já em formato de closure, ou seja, executadas e acessíveis através da nix store.

# Exemplos

- Derivações que baixam coisas da internet para poderem realizar este trabalho DEVEM ter o hash do arquivo baixado definido junto.
- Para compilar o Python é necessário um compilador de C, como por exemplo o GCC. Não é possível *realizar* a derivação do Python sem um compilador assumindo que a derivação do Python não vai baixar do cache.
- É possível usar o Nix para conversão de vídeos e para realizar a conversão em sí é necessário, por exemplo, um programa chamado [ffmpeg](https://ffmpeg.org/). Se a derivação do ffmpeg ainda não estiver realizada em uma closure não é possível iniciar a conversão.
- A closure de uma derivação pode ser exportada para outra máquina evitando assim que ela seja re-realizada, e é assim que caches binários funcionam.
