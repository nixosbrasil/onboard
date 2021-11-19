# Funções
Mesma ideia de outras linguagens. Perceba que não é possível alterar uma variável global por exemplo. Funções no Nix são [puras](https://pt.stackoverflow.com/questions/255557/o-que-%C3%A9-uma-fun%C3%A7%C3%A3o-pura) por definição. Ao passar um dado valor constante para uma função esta tem que retornar um outro valor constante, que pode ser o mesmo valor da entrada como é com a [função identidade](https://pt.wikipedia.org/wiki/Fun%C3%A7%C3%A3o_identidade).

No Nix as funções podem ter apenas um parâmetro e para ter o comporamento de funções de mais de um parâmetro é necessário definir uma função que retorna uma outra função que pega o próximo parâmetro.

Esta característica permite [aplicação parcial e currying](https://www.agatetepe.com.br/js-funcional-5-aplicacao-parcial-currying/) por padrão.

```nix
let
    sum = x: y: x + y;
in sum 2 2
```

