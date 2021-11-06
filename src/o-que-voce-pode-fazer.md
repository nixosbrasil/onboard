# O que eu posso fazer?

- Configurar ambientes de desenvolvimento e produção de forma automatizada e totalmente customizável sem ter que fazer gambiarras que não seriam automaticamente replicáveis quando for utilizar em uma outra máquina. (nix-shell, nix develop)

- Executar programas sem ter que instala-los globalmente primeiro. (nix-shell, nix run, nix develop)

- Executar o mesmo programa em versões diferentes sem que haja um conflito em relação ao local de instalação dos mesmos.

- Definir diretamente nos scripts as dependências destes que serão baixadas logo antes de executar os scripts. (shebang do nix-shell)

- Virtualização de programas apenas se o usuário desejar. Containers e VMs são virtualizados por via de regra, mesmo que containers não virtualizem o hardware. (tudo pode ser executado diretamente)

- Aproveitar dependências comuns entre programas sem gerar duplicidade de exatamente a mesma coisa. (derivations podem ter dependências em comum)

- Deduplicação a nível de arquivo dos arquivos gerados e baixados pelo Nix. (nix-store --optimize)

- Replicação de coisas repetitivas em configurações se baseando em alguma outra coisa ([exemplo do módulo do espanso](https://github.com/lucasew/nixcfg/blob/d7597a5288ee9b9e766ec18bfc874ad80a7e885c/homes/main/default.nix#L58))

- Distribuição Linux que pode ser totalmente declarativa, sem precisar refazer os passos da configuração em uma nova máquina. ([NixOS](https://nixos.org/))

- Wrappers customizados de programas já trazendo plugins e configuração. ([nix-vscode](https://github.com/lucasew/nix-vscode), [Neovim lucasew](https://github.com/lucasew/nixcfg/blob/d7597a5288ee9b9e766ec18bfc874ad80a7e885c/packages/custom/neovim/default.nix))

- Compilar o Android do seu celular. ([robotnix](https://github.com/danielfullmer/robotnix))

- Transformar basicamente qualquer tipo de arquivo em qualquer outro tipo contanto que obedeça a [lei da derivation](lei-da-derivation.md)
