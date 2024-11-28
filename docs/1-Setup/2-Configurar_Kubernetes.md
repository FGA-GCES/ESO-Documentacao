# Instalar e configurar Kubernets

Para mais detalhes checar [tutorial](https://github.com/leomichalski/kubernetes-para-devs/tree/main) e a [documentação oficial](https://kubernetes.io/docs/home/).


## Instalar Docker

```bash
curl -fsSL https://get.docker.com -o get-docker.sh
sh get-docker.sh

# testar
sudo docker version
```

## Instalar Kind (Kubernetes In Docker)

### Para Linux AMD64 / x86_64

```bash
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.23.0/kind-linux-amd64
chmod +x ./kind
sudo mv ./kind /usr/local/bin/kind

# testar
kind --version
```

### Para MacOs usando Homebrew

```bash
brew install kind

# testar
kind --version
```

Mais opções de instalação em <https://kind.sigs.k8s.io/docs/user/quick-start/#installation>

## Instalar kubectl

### Para Linux AMD64 / x86_64

```bash
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin/kubectl

# testar
kubectl version
```

### Para MacOs usando Homebrew

```bash
brew install kubectl

or

brew install kubernetes-cli

# testar
kubectl version --client
```

Mais opções de instalação em <https://kubernetes.io/docs/tasks/tools/#kubectl>

## Instalar Helm3

```bash
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
chmod 700 get_helm.sh
sh ./get_helm.sh

# testar
helm version
```

### Para MacOs usando Homebrew

```bash
brew install helm

# testar
helm version
```

Mais opções de instalação em <https://helm.sh/docs/intro/install/>

## Configuração do Kind

### Clonar este repositório e acessá-lo

```bash
git clone https://github.com/leomichalski/kubernetes-para-devs/tree/main
cd kubernetes-para-devs
```

### Navegar até a pasta principal do repositório

```bash
cd setup
```

### Começar cluster Kubernetes com Kind

```bash
kind create cluster --config kind_config.yaml
```

### Salver arquivo kubeconfig para poder usar o kubectl

```bash
kind get kubeconfig --name aula-gces | tee kubeconfig
```

### Testar kubectl

```bash
kubectl get nodes --kubeconfig kubeconfig
```