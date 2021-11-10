# Let

Uma das expressões mais úteis do Nix. Especialmente importante quando existe mais de uma operação na mesma linha e permite que uma operação seja feita em estágios, assim como pode ser usada como um bloco de escopo.

Na essência é como se fosse um attr, tem comportamento de attr, não permite loops de refência assim como attrsets porém o objetivo é construção do escopo local.

O modelo mental para entender a ideia é pensar tipo como teoremas são estruturados. Por exemplo:

> Seja x igual a 2 e y igual a 2, x somado a y resulta em ...

Em let expressions é

```nix
let
    x = 2;
    y = 2;
in x + y
```

Let, em conjunto com inherit e with pode ser usado para importar elementos para o escopo atual e estas capacidades serão abordadas logo em seguida.
