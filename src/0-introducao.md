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

## Nixpkgs

Existe uma coleção comunitária com mais de 80 mil pacotes Nix, que está configurada por padrão, chamada **[nixpkgs](https://search.nixos.org)**, às vezes referenciada apenas como **pkgs**. 


### NixOS

**[NixOS](https://nixos.org/)** é uma distribuição Linux de referência, construída com base no gerenciador Nix e nos pacotes do Nixpkgs.

NixOS é projetada como um conjunto de módulos que podem ser combinados pelo usuário, permitindo uma vasta gama de customizações, indo desde o gerenciador de boot e o kernel até desktops inteiros como o KDE Plasma e o Gnome.

Tal configuração não está limitada à simples instalação dos softwares, mas também se estende às suas configurações. Enquanto em distros tradicionais o usuário necessita editar arquivos espalhados pelo `/etc`, o sistema de módulos do NixOS também realiza esta configuração.

Grosso modo, o próprio NixOS é tratado como um pacote de software do ponto de vista do gerenciador Nix.

Uma propriedade interessante do sistema NixOS é o suporte à reversão (_rollback_), onde iterações anteriores (conhecidas como _gerações_) não são automaticamente apagadas, permanecendo disponíveis para serem utilizadas em caso de alguma falha na geração atual.


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
