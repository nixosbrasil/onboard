# Inherit

Provavelmente o que você está pensando é algo relacionado a herança e talvez esteja fazendo o link com linguagens orientadas a objeto. Na verdade o inherit é um [açucar sintático](https://pt.wikipedia.org/wiki/A%C3%A7%C3%BAcar_sint%C3%A1tico) para trazer membros de um outro escopo para o escopo atual.

Funciona apenas com attrs e expressões let, que são as formas que são usadas para implementar escopos em Nix, e pode ser expresso de algumas formas diferentes:

```nix
# Traz um valor do escopo atual para dentro do attr
{ inherit builtins; }

# Traz um membro de um attr no escopo para dentro do attr atual
{ inherit (builtins) fetchTarball map; }

# Exemplo usando expressões let
let
    inherit (builtins) sort;
    compara = a: b: a > b;
in sort compara [3 2 5 19 22 (-2)]

```

