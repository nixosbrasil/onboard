# inputs

Definições mais dentro do repositório devem evitar importar outros arquivos.

Porque? Loops!

E também porque não fica com um aspecto tão limpo.

Para utilizar as definições que usam este design pattern é usada a função `callPackage` do nixpkgs!

## Exemplo

### Antes da aplicação do design pattern
```nix
let
  pkgs = import <nixpkgs> {};
  mkDerivação = import ./autotools.nix pkgs;
in mkDerivação {
  name = "graphviz";
  src = ./graphviz-2.38.0.tar.gz;
  buildInputs = with pkgs; [ gd fontconfig libjpeg bzip2 ];
}
```
### Depois da aplicação do design pattern
```nix
{ mkDerivação, gdSupport ? true, gd, fontconfig, libjpeg, bzip2 }:

mkDerivação {
  name = "graphviz";
  src = ./graphviz-2.38.0.tar.gz;
  buildInputs = if gdSupport then [ gd fontconfig libjpeg bzip2 ] else [];
}
```
