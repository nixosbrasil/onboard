# Introdução

## O gerenciador de pacotes Nix

**[Nix](https://nixos.org/explore.html)** é um gerenciador de pacotes de software como dpkg/apt do Debian ou rpm do RedHat. Entretanto, assim como AppImage, Flatpack e Snap, pode ser instalado em *qualquer distribuição Linux*, e também em *Android*, *MacOS* ou *WSL*.

Nix tem um foco em _reproducibilidade_. Para isso, ele toma uma série de medidas, entre elas:

- separa a aquisição de fontes (código-fonte propriamente dito, _patches_ etc.) das demais fases de construção do pacote;
- exige verificação (mediante _hash sum_) das fontes adquiridas;
- impede o acesso à Internet durante a compilação do pacote;
- impede o acesso a arquivos e programas que não foram explicitamente requisitados como dependências;

Gerenciadores de pacotes tradicionais instalam seus pacotes diretamente na raiz do sistema, gerando arquivos espalhados em diversos diretórios.
Por outro lado, Nix instala cada pacote em um diretório dedicado, por padrão dentro de `/nix/store/`, em um formato similar a `/nix/store/<hash>-<nome do pacote>/{bin, lib, share, . . . }`


Este conjunto de medidas, bem como muitas outras, garante a reprodutibilidade da compilação. Em razão disso, é possível acelerar a compilação de pacotes ao mantê-los em um servidor de cache.
Por padrão, o projeto NixOS fornece o servidor [cache.nixos.org](https://cache.nixos.org), mas é perfeitamente possível configurar e utilizar outros.

## A Linguagem Nix

Para cada pacote são necessárias informações como nome, origem do código-fonte (caminho ou endereço online), versão (hash), dependências e instruções de compilação ou empacotamento. 

Essas informações devem ser descritas geralmente em um arquivo `default.nix` usando a linguagem programação de domínio especifico do Nix, também chamada **Nix** ou **Nix DSL**, é parecida com JSON, mas tem funções, variáveis pode importar outros arquivos Nix.

## Nixpkgs a coleção de pacotes

Existe uma coleção comunitária com mais de 80 mil pacotes Nix, que está configurada por padrão, chamada **[nixpkgs](https://search.nixos.org)**, às vezes referenciada apenas como **pkgs**. 

Apesar de todos pacotes estarem configurados, devido à linguagem Nix só ler que for de fato utilizado, nenhum destes pacotes será instalado em sua máquina a menos que usados como dependência de algum outro *pacote* ou um *pacote de ambiente* que esteja instalado.

### NixOS sistema operacional como *pacote de ambiente*

**[NixOS](https://nixos.org/download.html#nixos-iso)** é um pacote Nix contendo todas as dependências para se iniciar o *sistema operacional linux*, tal como kernel, grub ou efi e outras como systemd, xorg ou wayland, e ferramentas de reinstalação.

As configurações (ie. quase tudo que costuma ir no /etc), são pacotes e para facilitar a criação dos pacotes de configuração, foi criado um framework também usando a linguagem Nix, chamado **[Nix Modules](https://search.nixos.org/options)**, que permite usuário validar e reutilizar configurações para, por exemplo, criação de usuários, instalação pacotes e serviços.

A reconfiguração de NixOS na realidade é a geração de um novo pacote, referenciando todos pacotes e configurações (inalteradas e alteradas) e que é reinstalado. Como o pacote anterior não é automaticamente descartado, lhe será permitido reinstalar a versão anterior para casos de falha com a versão nova.

### HomeMananger configurações do usuário como *pacote de ambiente*

Utilizando o mesmo conceito do NixOS, **[HomeManager](https://github.com/nix-community/home-manager)** é um *pacote das configurações do usuário*, permitindo instalar pacotes ou configurações especificas para seu usuário, apesar de NixOS também permitir configurações por usuário, HomeManager pode ser instalado em outras distribuições, MacOS e WSL, além disto, possui algumas configurações únicas, sendo usado também em conjunto com NixOS.

### Projetos como *pacote de ambiente*

Caso um desenvolvedor de software, cientista de dados, ou qualquer profissional que precise *ferramentas diferentes para diferentes projetos* do dia a dia, é possível criar um *ambiente para cada projeto*, atualmente exitem diversas ferramentas, algumas usando Nix Modules como [DevEnv](https://github.com/cachix/devenv) e [DevShell](https://github.com/numtide/devshell) outras usando apenas pacotes como [DevBox](https://github.com/jetpack-io/devbox) e [Flox](https://github.com/flox/flox). Também é possível criar teu próprio ambiente apenas com Nix e Nixpkgs criando um arquivo `shell.nix` contendo as definições do teu pacote de ambiente.

Existe ainda a possibilidade de iniciar ambiente diretamente usando o comando `nix-shell -p DEPENDENCIA`.

### Outros… como *pacote*

Existem também algumas ferramentas para:

- Imagens OSI usadas por Docker, Kubernetes, etc.
- [Imagens de máquina virtual](https://github.com/nix-community/nixos-generators)>.
- Pacotes para dpkg/apt e rpm/yum.
- [Configurar qualquer outra distribuição Linux](https://github.com/numtide/system-manager)> da mesma forma que o NixOS.
