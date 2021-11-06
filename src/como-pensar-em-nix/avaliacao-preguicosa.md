# Avaliação preguiçosa

Nix, assim como linguagens como Haskell, possui avaliação preguiçosa, ou seja, os valores só são calculados quando acessados. Isso permite que o Nix só calcule expressões se estas forem pedidas.

Você pode imaginar um código Nix executando da mesma forma que imaginaria uma expressão matemática.

O Nix avalia as expressões de dentro para fora e é possível manipular esta ordem com parênteses por exemplo. Se a expressão não é referenciada ela não é executada.

Diferentemente de linguagens como Javascript e Python não é necessário encapsular um câlculo em uma função para ter este comporamento.

Pensa num código Nix como uma expressão matemática se abrindo e resolvendo de dentro para fora, se tal parte da expressão não é utilizada ela não vai ser calculada. Isso pode ser um tanto inconveniente para busca de erros pois um código só pode dar erro se for executado mas é essencial para o domínio que o Nix atende. Se Nix não fosse de avaliação preguiçosa todos teriam que baixar ou compilar o indice completo de definições de programas (nixpkgs) para poder usar qualquer coisa e isso definitivamente não seria legal.

## Exemplo

```nix
let
    a = 2 + 2;
    b = 4 + 4; # não é avaliado
in a
```

Esta lógica funciona desde em expressões que começam no mesmo arquivo até em valores que são gerados no decorrer de centenas ou mais de arquivos como é com o nixpkgs.
