# callPackage

Utilizando o design pattern `inputs` é necessário uma forma de acessar a definição no nível acima e é aí que entra a função `callPackage`.

Esta função consegue desmontar a função definida na definição usando o design pattern input passando valores padrão herdados do nixpkgs sendo utilizado e permite que sejam passados parâmetros extra, inclusive, sobrescrevendo os parâmetros originais.

A função `callPackage` pode ser deduzida da seguinte forma:

Sendo
- `set` o attr de entrada que contêm os valores padrões
- `f` a função importada da expressão usando o design pattern inputs
- `overrides` um attr com valores que serão alterados da entrada

```nix
callPackage = set: f: overrides: f ((builtins.intersectAttrs (builtins.functionArgs f) set) // overrides)
```

A versão do nixpkgs possui um comportamento levemente diferente.
- A função definida acima recebe como parâmetro `f` uma função que é a expressão utilizando o design pattern inputs
- A função do nixpkgs ao invés de uma função recebe um caminho para um arquivo nix, ou uma pasta, e realiza o import antes.
- A função acima recebe a função diretamente e a do nixpkgs recebe um caminho para o arquivo que importado entrega a função.
