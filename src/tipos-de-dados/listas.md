# Listas
Uma sequência de valores que podem ter tipos diferentes.

Assim como os attrsets, listas não podem ser modificadas depois de declaradas.

Para juntar duas listas é usado o operador `++`.

```nix
let
    a = [ 1 2 3 ];
    b = [ 4 5 6 ];
in a ++ b
```

