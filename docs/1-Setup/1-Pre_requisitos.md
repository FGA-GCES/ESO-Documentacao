# Pré-requisitos

## Instalar golang

- Instalar golang seguindo os passos em [link instalação golang](https://go.dev/doc/install).

## Instalar helm

```bash
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3

chmod 700 get_helm.sh

./get_helm.sh
```

- Outras opções de download checar [link](https://helm.sh/docs/intro/install/).

## Instalar yq

- Instalar binario do yq pelo [link](https://github.com/mikefarah/yq/releases/tag/v4.44.3) e descompactar.

- Problemas podem ocorrer instalando pelo binário, caso ocorram tente instalar pelo homebrew ou snap com os comandos:

```bash
brew install yq

ou

snap install yq
```

Para mais opções de download checar [repositório oficial yq.](https://github.com/mikefarah/yq)

## Instalar tilt

- Instalar tilt para poder desenvolver e verificar modificações no código seguindo o [link](https://tilt.dev/).