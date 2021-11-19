# Recursões

Assim como em outras linguagens funcionais, recursão é um padrão muito comum nos códigos e esta também acontece no Nix.

A recursão por definição precisa ter uma condição de parada e um passo recursivo. Se a condição de parada nunca para então tem-se um loop infinito e isso no Nix é um erro fatal e definitivamente o erro mais chato de se lidar da linguagem pois geralmente não é trivial rastrear a causa mas é possível replicar em exemplos simples como o seguinte:

```nix
let
    a = 2 + b;
    b = a + 1;
in a # pode ser o b também
```

Por Nix ser uma linguagem de avaliação preguiçosa meio que existe uma chamada de função implícita ao se acessar um valor e se acontece de ter um ciclo dá um problema conhecido como estouro de pilha, ou stack overflow.

Existem técnicas para evitar esses loops infinitos como os design patterns [callPackage](../design-patterns/callPackage.md) e [inputs](../design-patterns/inputs.md) e evitar o uso do [with](../expressoes/with.md) no topo do arquivo.

Além de reduzir a possibilidade de loops, técnicas assim permitem que loops sejam diagnosticados de uma forma bem mais simples.
