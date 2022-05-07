# A linguagem Nix

As operações realizadas pelo Nix gerenciador de pacote são definidas usando uma linguagem de programação também chamada de Nix.

Nix é uma linguagem de programação que possui as seguintes características:

* **Funcional**: a linguagem tem um comportamento de avaliação que lembra o de expressões matemáticas (declarativa) ao invés de uma sequência de passos (imperativa). Funções são tratadas como valores e como uma forma de criar blocos lógicos que podem ser reusados em outros locais. A imutabilidade permite um isolamento a nivel de função, o que permite uma segurança da pureza da função. Pureza significa determinismo, 2 + 2 vai ser sempre 4 independentemente de quando e onde esta operação for realizada. 
* **Imutável**: não é possível reatribuir estruturas. "Modificações" são feitas com transformações de dados e geralmente objetos entregam uma função, como a *override*, para poder gerar outro objeto com as alterações desejadas porém sem injetar nos mesmos locais que o objeto original estava. Se a é 2 não é possível reatribuir a 3, ou seja, não é possível modificar um valor por referência.
* **Tipagem dinâmica**: assim como linguagens como o Python, variáveis não são declaradas com um tipo específico. Listas e attribute sets podem ter itens com tipos diferentes e não são tipados.
* **Interpretada**: o texto das expressões não é previamente compilado em um executável e então executado. Operações de transformação de arquivos geram arquivos de *derivation*, que é o mais próximo de compilação que a linguagem Nix realiza. 
