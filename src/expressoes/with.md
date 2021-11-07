# With

Uma outra forma de trazer itens de outros escopos para o atual é o with. Fazendo o link com o Python, seria um equivalente a um `from x import *`.

Esta primitiva não pode ser usada em attrs e é sempre seguida de uma expressão.

## Exemplo

Traz o escopo builtins para o escopo da expressão em seguida que acessa o item head, que implicitamente referencia `builtins.head`
```nix
with builtins; head
```

## Aviso
With tem uso desencorajado, principalmente em topo de arquivo pois pode facilitar a ocorrência de loops e dificuldades no rastreamento destes. Um código evitando withs tende a ser um código mais limpo e fácil de manter no longo prazo.

Um jeito comum de lidar com isso é usar uma let expression com inherits trazendo apenas o necessário dos escopos. No nixpkgs isso é bem evidente e existem vários exemplos reais bem simples de entender na pasta `lib`.
