# With

Uma outra forma de trazer itens de outros escopos para o atual é o with. Fazendo o link com o Python, seria um equivalente a um `from x import *`.

Esta primitiva não pode ser usada como um valor mas sim como um prefixo para uma expressão que depende desse escopo repassado.

## Exemplo

With não pode ser usado dentro de attrsets e let expressions como valor.

```nix
{ with builtins; } # Não funciona
let with builtins; in head # Não funciona
```

Se o usuário quer juntar um attrset especificado com outro pode usar o operador `//`!.

Traz o escopo builtins para o escopo da expressão em seguida que acessa o item head, que implicitamente referencia `builtins.head`
```nix
with builtins; head
```

## Aviso
With tem uso desencorajado, principalmente no topo de arquivo pois impossibilita a análise estática da linguagem, resultando em erros mais genéricos e difíceis de resolver. Um código evitando withs tende a ser um código mais fácil de manter no longo prazo.

Um jeito comum de lidar com isso é usar uma let expression com inherits trazendo apenas o necessário dos escopos. No nixpkgs isso é bem evidente e existem vários exemplos reais bem simples de entender na pasta `lib`.
