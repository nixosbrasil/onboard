# Textuais
Strings, assim como em outras linguagens.

Strings podem ser declaradas entre aspas (`"`) ou entre duas aspas simples (`''`). 

As duas suportam mais de uma linha, a conveniência da sintaxe com duas aspas simples é lidar com conflitos ao escrever scripts. Aspas duplas são muito usadas no Shell Script e um caso de uso comum é usar o Nix para gerar scripts customizados.

Para juntar duas strings é possível somar ou interpolar elas.

```nix
let
    str_a = "hello";
    str_b = "world";
in {
    str_soma = str_a + str_b; # "helloworld";
    str_interpolacao = "${str_a} ${str_b}";
}
```


