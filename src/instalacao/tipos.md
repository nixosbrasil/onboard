# Tipos de instalação

No Nix existem dois tipos de instalação e a diferença dos dois, além do comando de instalação, está no modelo de segurança empregado.

## Single user mode

Ou usuário único, apenas um usuário pode operar o Nix na máquina. É o jeito padrão apresentado no [site](https://nixos.org/download.html). Por padrão é o usuário que está chamando o instalador. É mais simples mas se mais de um usuário na máquina utilizar, o modelo de multiusuário é mais indicado.

A /nix no modo de um usuário é atribuída ao usuário que instalou.

## Multi user mode

Ou modo de multiusuário, permite que mais de um usuário no sistema possa utilizar o Nix.

Para permitir que uma Nix store seja compartilhada de forma segura entre usuários é importante que usuários não possam rodar builders que alterem a Nix store e o banco de dados do Nix de forma arbitrária porque se puderem poderiam instalar um trojan (cavalo de troia), por exemplo, no sistema e comprometer as contas dos outros usuários.

Para evitar este problema a Nix store e o banco de dados são atribuídos a um usuário privilegiado, geralmente o root, e os builders são executados por usuários especiais, geralmente chamados de nixbld1, nixbld2 e assim por diante.

Quando um usuário do sistema usa o Nix, operações que lidam com a Nix store, como realizations, são enviadas para um daemon do Nix executando na máquina.

Por ser um tanto mais crítica essa questão de segurança apenas usuários confiáveis e usuários pertencentes a grupos confiáveis podem realizar tarefas mais administrativas como especificar caches binários.

Apesar das restrições, usuários normais podem realizar derivations, e consequentemente, instalar pacotes e ambientes sem precisar de alguma permissão administrativa.
