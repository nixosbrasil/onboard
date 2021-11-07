# [lucasew](https://github.com/lucasew/nixcfg/)

Possui
- Exemplo de definição usando home-manager (homes)
- Exemplo de definição de máquina usando NixOS (nodes)
- Exemplo de extensão de uma definição base (nodes/{bootstrap,common})
- Uso de flakes (flake.nix)
- Uma área de compat para facilitar referências usando o Nix sem flakes
- Funções utilitárias que são carregadas usando a funcionalidade de overlay
- Alguns programas que não estão no Nixpkgs empacotados por fora e acessíveis por overlay
- Gitignore na pasta secrets, onde ficam valores secretos como chaves de API, estes arquivos secretos não vão ser commitados junto com o resto do repositório
- Um arquivo authorized_keys com a chave pública das máquinas para autorizar facilmente em máquinas novas (authorized_keys)
- Um script para aplicar o formatador automático ao repositório (format.sh)
- Um arquivo nur.nix usado pelo bot do NUR para indexar o repositório
- Fundo da área de trabalho (wall.jpg)
- Configurações para poder usar o GitHub Actions para precompilar gerações depois de atualizar o Nixpkgs
    - Existem algumas customizações em alguns pacotes que são compiladas sempre que o nixpkgs é atualizado então antes de aplicar a geração localmente é chamado um job do Github Actions que compila a nova geração e manda para o Cachix, quando este job termina é aplicada a nova geração localmente e ao invés de compilar a estes pacotes modificados é apenas baixada a closure do Cachix.
