# override

Uma forma de gerar uma nova attrset utilizando partes da attrset anterior. 

Muito comum em customizações de programas já definidos, como por exemplo usar a definição fornecida pelo Nixpkgs do kernel Linux e com isso poder passar modificações para este de uma forma que o usuário não seja obrigado a adotar essa definição ou acabar tendo surpresas pelo gerenciador de pacotes da distribuição ter sobrescrito aquele pacote modificado pelo padrão.

Essa abordagem pode inclusive funcionar com alterações vindo de novas versões do Nixpkgs passando sempre um mesmo patch no código de entrada.

E o princípio por trás desta técnica está em attrsets que podem ser recriadas passando um conjunto de alterações e a técnica é chamada de override.

Overrides podem ser implementados como funções e uma forma de deduzir é:

```
let
    makeOverridable = f: origArgs:
        let
            origRes = f origArgs;
        in
            origRes // { override = newArgs: makeOverridable f (origArgs // newArgs); };
in makeOverridable (v: v) {}
```

Neste caso a expressão vai retornar um attrset com um item `override` com uma função.

Para poder experimentar as possibilidades abra o `nix-repl` pelo terminal e digite `v = ` seguido do código acima, o resultado da expressão vai ficar na variável v.

Experimente expressões como a seguinte:
```nix
(v.override {hello = "world";}).override {foo = "bar";}
```

## Aviso
No nixpkgs são usados dois tipos de overrides nos pacotes.

- O `override` muda os parâmetros da função que é definida seguindo o design pattern `[inputs](./inputs.md)`.
- O `overrideAttrs` muda os parâmetros passados para a função primitiva que gera a derivação, chamada de `mkDerivation`.
