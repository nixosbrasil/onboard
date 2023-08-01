# Introdução

## Nix o gerenciador de pacotes

**[Nix](https://nixos.org/explore.html)**<sup>🇬🇧</sup> é um gerenciador de pacotes de software como dpkg/apt do Debian ou rpm do RedHat. Entretanto, assim como AppImage, Flatpack e Snap, pode ser instalado em *qualquer distribuição Linux*, e também em *Android*, *MacOS* ou *WSL*.

Seu principal foco é que os pacotes sejam 100% reproduzíveis, para isso isola a compilação do pacote, não permitindo acesso à internet, bibliotecas ou ferramentas externas que não possuam versão (hash) ou não estejam declaradas como dependência. 

Também tenta isolar as dependências no momento da execução, por isso ao invés de usar as dependências de um diretório único compartilhado como */lib* usa vários diretórios com hash das dependencias */nix/store/HASH-DEPENDENCIA/lib*, permitindo diferentes versões da mesma dependência, trocando conflitos por duplicidade.

A reproduzibilidade e o isolamento, permitem que qualquer máquina com Nix e SSH sejam utilizadas para gerar os pacotes, permitindo escalar a quantidade de empacotadores e deixar que outras maquinas mais potentes produzam o pacote caso seja um processo intensivo, como a compilação de código.

Pode have ainda um terceiro servidor especializado em hospedar os pacotes, o padrão é [cache.nixos.org](https://cache.nixos.org)<sup>🇬🇧</sup> que possui cache de boa parte pacotes de nixpkgs, porém, é possível configurar teu próprio utilizando outra máquina com SSH, HTTP ou API do S3.

## Nix a linguagem

Para cada pacote são necessárias informações como nome, origem do código-fonte (caminho ou endereço online), versão (hash), dependências e instruções de compilação ou empacotamento. 

Essas informações devem ser descritas geralmente em um arquivo `default.nix` usando a linguagem programação de domínio especifico do Nix, também chamada **Nix** ou **Nix DSL**, é parecida com JSON, mas tem funções, variáveis pode importar outros arquivos Nix.

## Nixpkgs a coleção de pacotes

Existe uma coleção comunitária com mais de 80 mil pacotes Nix, que está configurada por padrão, chamada **[nixpkgs](https://search.nixos.org)**<sup>🇬🇧</sup>, às vezes referenciada apenas como **pkgs**. 

Apesar de todos pacotes estarem configurados, devido à linguagem Nix só ler que for de fato utilizado, nenhum destes pacotes será instalado em sua máquina a menos que usados como dependência de algum outro *pacote* ou um *pacote de ambiente* que esteja instalado.

### NixOS sistema operacional como *pacote de ambiente*

**[NixOS](https://nixos.org/download.html#nixos-iso)**<sup>🇬🇧</sup> é um pacote Nix contendo todas as dependências para se iniciar o *sistema operacional linux*, tal como kernel, grub ou efi e outras como systemd, xorg ou wayland, e ferramentas de reinstalação.

As configurações (ie. quase tudo que costuma ir no /etc), são pacotes e para facilitar a criação dos pacotes de configuração, foi criado um framework também usando a linguagem Nix, chamado **[Nix Modules](https://search.nixos.org/options)**<sup>🇬🇧</sup>, que permite usuário validar e reutilizar configurações para, por exemplo, criação de usuários, instalação pacotes e serviços.

A reconfiguração de NixOS na realidade é a geração de um novo pacote, referenciando todos pacotes e configurações (inalteradas e alteradas) e que é reinstalado. Como o pacote anterior não é automaticamente descartado, lhe será permitido reinstalar a versão anterior para casos de falha com a versão nova.

### HomeMananger configurações do usuário como *pacote de ambiente*

Utilizando o mesmo conceito do NixOS, **[HomeManager](https://github.com/nix-community/home-manager)**<sup>🇬🇧</sup> é um *pacote das configurações do usuário*, permitindo instalar pacotes ou configurações especificas para seu usuário, apesar de NixOS também permitir configurações por usuário, HomeManager pode ser instalado em outras distribuições, MacOS e WSL, além disto, possui algumas configurações únicas, sendo usado também em conjunto com NixOS.

### Projetos como *pacote de ambiente*

Caso um desenvolvedor de software, cientista de dados, ou qualquer profissional que precise *ferramentas diferentes para diferentes projetos* do dia a dia, é possível criar um *ambiente para cada projeto*, atualmente exitem diversas ferramentas, algumas usando Nix Modules como [DevEnv](https://github.com/cachix/devenv)<sup>🇬🇧</sup> e [DevShell](https://github.com/numtide/devshell)<sup>🇬🇧</sup> outras usando apenas pacotes como [DevBox](https://github.com/jetpack-io/devbox)<sup>🇬🇧</sup> e [Flox](https://github.com/flox/flox)<sup>🇬🇧</sup>. Também é possível criar teu próprio ambiente apenas com Nix e Nixpkgs criando um arquivo `shell.nix` contendo as definições do teu pacote de ambiente.

Existe ainda a possibilidade de iniciar ambiente diretamente usando o comando `nix-shell -p DEPENDENCIA`.

### Outros… como *pacote*

Existem também algumas ferramentas para:

- Imagens OSI usadas por Docker, Kubernetes, etc.
- [Imagens de máquina virtual](https://github.com/nix-community/nixos-generators)<sup>🇬🇧</sup>.
- Pacotes para dpkg/apt e rpm/yum.
- [Configurar qualquer outra distribuição Linux](https://github.com/numtide/system-manager)<sup>🇬🇧</sup> da mesma forma que o NixOS.
