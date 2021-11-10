# Attrs
Equivalentes a objetos do Javascript ou dicionários do Python, porém não podem ser modificados depois de declarados.

Para juntar dois attrsets é usado o operador `//`.

```nix
let
    a = { linguagem = "Nix"; };
    b = { versao = "2.4"; };
in a // b
```

Também é possível especificar attrsets aninhados usando duas formas que podem ser interutilizadas sem problemas.

```nix
let
    a = {
        linguagem.nome = "Nix";
        linguagem.versao = "2.4";
    };
    b = {
        linguagem = {
            nome = "Nix";
            versao = "2.4";
        };
    };
in {
    inherit a b;
};
```


