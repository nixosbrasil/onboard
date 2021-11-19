# Analogia: _hashmap_ vs árvore

Em estrutura de dados busca-se formas de guardar dados na memória a fim de poder recuperá-los de forma mais eficiente. Não nos 
aprofundaremos tanto neste assunto, somente o que for pertinente neste caso.

## O que é uma _hashmap_/_hashtable_/tabela hash?

Se você já programou Python você conhece pelo nome de dicionário, a ideia é basicamente a mesma.

É uma estrutura de dados em que o programador pode associar um valor a uma chave e depois pode recuperar este mesmo valor partindo desta chave.

![Exemplo do wikipédia para deixar mais ilustrativo](assets/315px-Hash_table_3_1_1_0_1_0_0_SP.svg.png)

## O que é uma árvore?

É uma estrutura de dados hierárquica, ou seja, tem um ponto mais alto, que se divide entre `n` caminhos. É composta por nós e arestas. O nó mais alto é o nó raiz, já o nó que não possui filhos é chamado de nó folha. Existem vários tipos de árvores, a mais conhecida é a árvore binária em que cada nó tem até dois nós filhos. Para a nossa analogia assuma que um nó pode ter quantos filhos forem necessários.

![Exemplo de árvore binária](assets/binary_tree-1.png)

## O que isso tem a ver com Nix?

Como gerenciadores de pacotes tradicionais gerenciam pacotes? Mais especificamente, como eles aplicam atualizações?

Eu, @lucasew, ja usei Arch Linux por aproximandamente um ano e naquele tempo eu usava um setup com i3wm + [polybar](https://aur.archlinux.org/packages/polybar/). A questão é que o polybar depende de uma biblioteca chamada [jsoncpp](https://archlinux.org/packages/extra/x86_64/jsoncpp/) e vivia quebrando por causa desta bibiliteca. Por quê?

A cada atualização de pacote esta biblioteca virava um arquivo diferente e, consequentemente, o polybar tinha que ser atualizado para procurar pelo novo nome. Mensalmente, quando eu atualizava, o polybar simplesmente se recusava de abrir e aí é que reside a analogia do _hashmap_.

Quando um pacote é atualizado pelo pacman a versão nova é sobrescrita em cima da antiga e qualquer coisa que assuma algum detalhe de uma versão em específico vai quebrar, e esse é o perigo da mutabilidade.

O Nix não tem esse problema.

Ao invés do pacote polybar depender do jsoncpp, uma derivação que compilará o polybar dependerá da derivação que compila o jsoncpp. Caso o jsoncpp atualize, a derivação do polybar será alterada por consequência.

![Exemplo que pode ser encontrado na tese sobre o NixOS](assets/ex-nix-path-tese-nixos.png)
