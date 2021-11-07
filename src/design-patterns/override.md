# override

Uma forma de gerar uma nova attr utilizando partes da attr anterior. 

Muito comum em customizações de programas já definidos, como por exemplo usar a definição fornecida pelo Nixpkgs do kernel Linux e com isso poder passar modificações para este de uma forma que o usuário não seja obrigado a adotar essa definição ou acabar tendo surpresas pelo gerenciador de pacotes da distribuição ter sobrescrito aquele pacote modificado pelo padrão.

Essa abordagem pode inclusive funcionar com alterações vindo de novas versões do Nixpkgs passando sempre um mesmo patch no código de entrada.

E o princípio por trás desta técnica está em attrs que podem ser recriadas passando um conjunto de alterações e a técnica é chamada de override.

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

Neste caso a expressão vai retornar um attr com um item `override` com uma função.

Para poder experimentar as possibilidades abra o `nix-repl` pelo terminal e digite `v = ` seguido do código acima, o resultado da expressão vai ficar na variável v.

Experimente expressões como a seguinte:
```nix
(v.override {hello = "world";}).override {foo = "bar";}
```
