# Inherit

Provavelmente o que você está pensando é algo relacionado a herança e talvez esteja fazendo o link com linguagens orientadas a objeto. Na verdade o inherit é um [açucar sintático](https://pt.wikipedia.org/wiki/A%C3%A7%C3%BAcar_sint%C3%A1tico) para trazer membros de um outro attr para o attr atual.

Funciona apenas com attrs e pode ser expresso de algumas formas diferentes:

```nix
# Traz um valor do escopo atual para dentro do attr
{ inherit builtins; }

# Traz um membro de um attr no escopo para dentro do attr atual
{ inherit (builtins) fetchTarball map; }

O inherit também funciona em expressões let!
```

