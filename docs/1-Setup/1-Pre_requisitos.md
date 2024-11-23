# Pré-requisitos

Para colaborar com o projeto [External Secrets Operator (ESO)](https://external-secrets.io/latest/), é necessário instalar algumas ferramentas no computador. Neste guia, será explicado o que é cada ferramenta, por que é necessária, a versão recomendada e como instalá-la no sistema operacional correspondente.

## Sistemas Operacionais Suportados

Para colaborar com o projeto **External Secrets Operator (ESO)**, é recomendado utilizar sistemas operacionais baseados em Unix, como **Linux** e **macOS**. O ambiente de desenvolvimento do ESO é principalmente voltado para esses sistemas, e muitas das ferramentas e scripts utilizados no desenvolvimento são projetados para funcionar neles.

### É possível desenvolver no Windows?

É possível utilizar o Windows para o desenvolvimento, mas há considerações importantes a serem feitas. Como o ambiente de desenvolvimento do ESO não é otimizado para o Windows, podem surgir problemas de incompatibilidade com ferramentas como **Make**, **Tilt** e scripts shell. Os scripts de automação e comandos presentes no projeto são escritos para ambientes Unix, utilizando bash scripting, o que pode não ser compatível com o Windows sem adaptações. Este tutorial não cobrirá a instalação e configuração de ferramentas no Windows devido à complexidade e falta de testes.

---

## Instalar Go (Golang)

<details>
  <summary>Sobre o Golang</summary>

### O que é Go?

Go, também conhecido como Golang, é uma linguagem de programação criada pelo Google. É conhecida por ser eficiente, fácil de aprender e excelente para desenvolver aplicativos rápidos e escaláveis.

### Por que é necessário Go?

No projeto **External Secrets Operator**, Go é utilizado para desenvolver partes fundamentais do código. É necessário para compilar, executar e contribuir com o código-fonte do projeto.

</details>

<details>
  <summary>Instalação do Golang</summary>

### Versão Necessária

- **Versão mínima:** Go 1.20 ou superior.
- **Versão recomendada:** Go 1.23.3

> Durante o desenvolvimento deste guia, a versão mais recente do Go é a **1.23.3**, a qual funcionou perfeitamente com o projeto **External Secrets Operator**. Versões anteriores apresentaram falhas nos testes da aplicação. Antes de testar o projeto, verifique sua versão do Go.

### Como Instalar Go

<details>
  <summary>Instalação no Linux</summary>

1. **Baixar o arquivo de instalação do Go:**

   Acesse o site oficial ou use o comando abaixo:

   ```bash
   wget https://golang.org/dl/go1.23.3.linux-amd64.tar.gz
   ```

2. **Remover instalações anteriores do Go:**

   ```bash
   sudo rm -rf /usr/local/go
   ```

3. **Extrair o novo arquivo do Go para `/usr/local`:**

   ```bash
   sudo tar -C /usr/local -xzf go1.23.3.linux-amd64.tar.gz
   ```

4. **Atualizar o PATH adicionando `/usr/local/go/bin`:**

   - Edite o arquivo `~/.profile` ou `/etc/profile` e adicione:

     ```bash
     export PATH=$PATH:/usr/local/go/bin
     ```

   - Ou execute diretamente no terminal para a sessão atual:

     ```bash
     export PATH=$PATH:/usr/local/go/bin
     ```

5. **Aplicar as alterações do PATH imediatamente:**

   ```bash
   source ~/.profile
   ```

6. **Verificar a instalação do Go e se está na versão suportada:**

   ```bash
   go version
   ```

> **Nota:** Para Debian/Ubuntu, é possível instalar o Go utilizando o Snap:

```bash
sudo snap install --classic go
```

</details>

<details>
  <summary>Instalação no macOS</summary>

1. **Baixar o arquivo de instalação do Go:**

   - [Apple macOS (ARM64), macOS 11 ou superior](https://go.dev/dl/go1.23.3.darwin-arm64.pkg)
   - [Apple macOS (Intel), macOS 10.15 ou superior](https://go.dev/dl/go1.23.3.darwin-amd64.pkg)

2. **Executar o arquivo baixado e seguir as instruções de instalação.**

   O pacote instala a distribuição do Go em `/usr/local/go`. O instalador deve adicionar o diretório `/usr/local/go/bin` à variável de ambiente `PATH`. Pode ser necessário reiniciar qualquer sessão aberta do Terminal para que a alteração entre em vigor.

3. **Verificar a instalação do Go e se está na versão suportada:**

   ```bash
   go version
   ```

</details>

Quaisquer dúvidas ou problemas com a instalação do Go, consulte a [documentação oficial](https://go.dev/doc/install).

---
</details>

## Instalar Helm

<details>
  <summary>Sobre o Helm</summary>

### O que é o Helm?

O Helm é um gerenciador de pacotes para Kubernetes, a plataforma que automatiza a implantação, escalonamento e gerenciamento de aplicativos em contêineres.

### Por que é necessário o Helm?

No projeto **External Secrets Operator**, o Helm é utilizado para simplificar a instalação e gerenciamento de aplicações dentro do Kubernetes, automatizando processos complexos de configuração e implantação.

</details>

<details>
  <summary>Instalação do Helm</summary>

### Versão Necessária

- **Versão recomendada:** Helm 3 (versão mais recente do Helm 3).

### Como Instalar o Helm

<details>
  <summary>Instalação no Linux</summary>

1. **Baixar o script de instalação:**

   ```bash
   curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
   ```

2. **Tornar o script executável:**

   ```bash
   chmod 700 get_helm.sh
   ```

3. **Executar o script de instalação:**

   ```bash
   ./get_helm.sh
   ```

4. **Verificar a instalação do Helm:**

   ```bash
   helm version
   ```

</details>

<details>
  <summary>Instalação no macOS</summary>

- **Usando o Homebrew:**

  ```bash
  brew install helm
  ```

- **Verificar a instalação do Helm:**

  ```bash
  helm version
  ```

</details>

Para outras opções de instalação e mais detalhes, consulte o [guia oficial de instalação do Helm](https://helm.sh/docs/intro/install/).

</details>

---

## Instalar yq

<details>
  <summary>Sobre o yq</summary>

### O que é o yq?

O yq é uma ferramenta de linha de comando para ler, manipular e escrever arquivos YAML, amplamente utilizados para configurações.

### Por que é necessário o yq?

No projeto **External Secrets Operator**, o yq é utilizado para automatizar a edição de arquivos de configuração YAML, facilitando ajustes e implementações.

</details>

<details>
  <summary>Instalação do yq</summary>

### Versão Necessária

- **Versão recomendada:** yq v4.44.3 ou superior.

### Como Instalar o yq

<details>
  <summary>Instalação no Linux</summary>

1. **Baixar o binário do yq:**

   ```bash
   wget https://github.com/mikefarah/yq/releases/download/v4.44.3/yq_linux_amd64.tar.gz
   ```

2. **Extrair o arquivo baixado:**

   ```bash
   tar xvf yq_linux_amd64.tar.gz
   ```

3. **Mover o binário para `/usr/local/bin` e tornar executável:**

   ```bash
   sudo mv yq_linux_amd64 /usr/local/bin/yq
   sudo chmod +x /usr/local/bin/yq
   ```

4. **Verificar a instalação do yq:**

   ```bash
   yq --version
   ```

> **Alternativa:** Caso encontre problemas, instale via Snap:

```bash
sudo snap install yq
```

</details>

<details>
  <summary>Instalação no macOS</summary>

- **Usando o Homebrew:**

  ```bash
  brew install yq
  ```

- **Verificar a instalação do yq:**

  ```bash
  yq --version
  ```

</details>

Para outras opções de instalação e mais detalhes, consulte o [repositório oficial do yq](https://github.com/mikefarah/yq).

</details>

---

## Instalar jq

<details>
  <summary>Sobre o jq</summary>

### O que é o jq?

O jq é uma ferramenta de linha de comando para processar e manipular dados em formato JSON.

### Por que é necessário o jq?

No projeto **External Secrets Operator**, o jq é essencial para trabalhar com dados JSON, permitindo filtrar e transformar informações de forma eficiente.

</details>

<details>
  <summary>Instalação do jq</summary>

### Versão Necessária

- **Versão recomendada:** jq 1.6 ou superior.

### Como Instalar o jq

<details>
  <summary>Instalação no Linux</summary>

- **Para Debian/Ubuntu:**

  ```bash
  sudo apt-get install jq
  ```

- **Para Fedora:**

  ```bash
  sudo dnf install jq
  ```

- **Verificar a instalação do jq:**

  ```bash
  jq --version
  ```

</details>

<details>
  <summary>Instalação no macOS</summary>

- **Usando o Homebrew:**

  ```bash
  brew install jq
  ```

- **Verificar a instalação do jq:**

  ```bash
  jq --version
  ```

</details>

Para outras opções de instalação e mais detalhes, consulte o [site oficial do jq](https://stedolan.github.io/jq/).

</details>

---

## Instalar Docker

<details>
  <summary>Sobre o Docker</summary>

### O que é o Docker?

O Docker é uma plataforma que permite criar, implantar e executar aplicativos em contêineres. Os contêineres permitem empacotar uma aplicação com todas as suas dependências em uma unidade padrão para desenvolvimento e implantação.

### Por que é necessário o Docker?

No projeto **External Secrets Operator**, o Docker é usado para criar imagens de contêineres e executar serviços em ambientes isolados. É essencial para o desenvolvimento, teste e implantação da aplicação dentro de um ambiente Kubernetes.

</details>

<details>
  <summary>Instalação do Docker</summary>

### Como Instalar o Docker

<details>
  <summary>Instalação no Linux</summary>

1. **Atualizar os pacotes existentes:**

   ```bash
   sudo apt-get update
   ```

2. **Instalar pacotes necessários:**

   ```bash
   sudo apt-get install \
     ca-certificates \
     curl \
     gnupg \
     lsb-release
   ```

3. **Adicionar a chave GPG oficial do Docker:**

   ```bash
   curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
   ```

4. **Adicionar o repositório do Docker:**

   ```bash
   echo \
     "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] \
     https://download.docker.com/linux/ubuntu \
     $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
   ```

5. **Instalar o Docker Engine:**

   ```bash
   sudo apt-get update
   sudo apt-get install docker-ce docker-ce-cli containerd.io
   ```

6. **Verificar a instalação do Docker:**

   ```bash
   sudo docker run hello-world
   ```

</details>

<details>
  <summary>Instalação no macOS</summary>

- **Baixar o Docker Desktop para macOS:**

  Acesse o site oficial e baixe o Docker Desktop:

  - [Docker Desktop para Mac com Intel Chip](https://desktop.docker.com/mac/stable/amd64/Docker.dmg)
  - [Docker Desktop para Mac com Apple Chip (M1)](https://desktop.docker.com/mac/stable/arm64/Docker.dmg)

- **Instalar o Docker Desktop:**

  1. Abra o arquivo `Docker.dmg`.
  2. Arraste o ícone do Docker para a pasta `Applications`.
  3. Inicie o Docker Desktop a partir da pasta `Applications`.

- **Verificar a instalação do Docker:**

  Abra um terminal e execute:

  ```bash
  docker --version
  ```

</details>

Para outras opções de instalação e mais detalhes, consulte a [documentação oficial do Docker](https://docs.docker.com/get-docker/).

</details>

<details>
  <summary>Configuração necessária no Docker</summary>

### Configurar Docker para Uso sem Root

Por padrão, o Docker requer privilégios de superusuário (root) para executar. Para facilitar o uso, é recomendado adicionar o usuário atual ao grupo `docker` para executar comandos sem `sudo`.

<details>
  <summary>Passos para configurar o Docker sem root no Linux</summary>

1. **Criar o grupo docker (se não existir):**

   ```bash
   sudo groupadd docker
   ```

2. **Adicionar o usuário atual ao grupo docker:**

   ```bash
   sudo usermod -aG docker $USER
   ```

3. **Aplicar as alterações de grupo sem fazer logout:**

   ```bash
   newgrp docker
   ```

4. **Verificar se é possível executar o Docker sem sudo:**

   ```bash
   docker run hello-world
   ```

   Se o comando funcionar sem erros, a configuração foi bem-sucedida.

</details>

</details>
  
---

## Instalar kubectl

<details>
  <summary>Sobre o Kubectl</summary>

### O que é o kubectl?

O **kubectl** é a ferramenta de linha de comando para gerenciar clusters Kubernetes. Permite executar comandos no cluster, gerenciar recursos e depurar aplicações.

### Por que é necessário o kubectl?

No projeto **External Secrets Operator**, o kubectl é usado para interagir com o cluster Kubernetes local ou remoto, aplicar configurações e verificar o estado dos recursos implantados.

</details>

<details>
  <summary>Instalação do kubectl</summary>

### Versão Necessária

- **Versão compatível com a versão do Kubernetes instalada (geralmente a versão estável mais recente).**

### Como Instalar o kubectl

<details>
  <summary>Instalação no Linux</summary>

1. **Baixar a versão mais recente do kubectl:**

   ```bash
   curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
   ```

2. **Tornar o binário executável:**

   ```bash
   chmod +x kubectl
   ```

3. **Mover o binário para o PATH:**

   ```bash
   sudo mv kubectl /usr/local/bin/
   ```

4. **Verificar a instalação do kubectl:**

   ```bash
   kubectl version --client
   ```

</details>

<details>
  <summary>Instalação no macOS</summary>

- **Usando o Homebrew:**

  ```bash
  brew install kubectl
  ```

- **Verificar a instalação do kubectl:**

  ```bash
  kubectl version --client
  ```

</details>

Para outras opções de instalação e mais detalhes, consulte a [documentação oficial do kubectl](https://kubernetes.io/docs/tasks/tools/).

</details>

---

## Instalar ctlptl e criar um cluster Kind com registro local

<details>
  <summary>Sobre o ctlptl</summary>

### O que é o ctlptl?

O **ctlptl** (Control Plane Tool) é uma ferramenta para gerenciar clusters locais de desenvolvimento Kubernetes. Ele facilita a criação e gerenciamento de clusters como o **Kind** (Kubernetes in Docker) e a configuração de registros locais de contêiner.

### Por que é necessário o ctlptl?

No projeto **External Secrets Operator**, o ctlptl é usado para criar e gerenciar um cluster Kubernetes local usando o Kind, além de configurar um registro local de contêiner para armazenar imagens Docker durante o desenvolvimento.

</details>

<details>
  <summary>Instalação do ctlptl</summary>

### Versão Necessária

- **Versão mais recente disponível do ctlptl.**

### Como Instalar o ctlptl

<details>
  <summary>Instalação no Linux</summary>

1. **Baixar o binário do ctlptl:**

   ```bash
   curl -s https://api.github.com/repos/tilt-dev/ctlptl/releases/latest \
   | grep "browser_download_url.*linux_amd64.tar.gz" \
   | cut -d '"' -f 4 \
   | wget -i -
   ```

2. **Extrair o arquivo baixado:**

   ```bash
   tar xvf ctlptl*_linux_amd64.tar.gz
   ```

3. **Mover o binário para `/usr/local/bin`:**

   ```bash
   sudo mv ctlptl /usr/local/bin/
   ```

4. **Verificar a instalação do ctlptl:**

   ```bash
   ctlptl version
   ```

</details>

<details>
  <summary>Instalação no macOS</summary>

- **Usando o Homebrew:**

  ```bash
  brew install tilt-dev/tap/ctlptl
  ```

- **Verificar a instalação do ctlptl:**

  ```bash
  ctlptl version
  ```

</details>

</details>

### Criar um Cluster Kind com Registro Local

<details>
  <summary>Sobre o Kind</summary>

O **Kind** (Kubernetes in Docker) é uma ferramenta para executar clusters Kubernetes locais usando contêineres Docker como nós do cluster.

</details>

<details>
  <summary>Como Criar um Cluster Kind com Registro Local</summary>

1. **Criar um registro local de contêiner:**

   ```bash
   docker run -d --restart=always -p "5000:5000" --name kind-registry registry:2
   ```

2. **Criar um cluster Kind usando o ctlptl e conectá-lo ao registro local:**

   ```bash
   ctlptl create cluster kind --registry=kind-registry
   ```

   Isso criará um cluster Kind configurado para usar o registro local em `localhost:5000`.

3. **Verificar se o cluster está funcionando:**

   ```bash
   kubectl cluster-info --context kind-kind
   ```

4. **Listar os clusters gerenciados pelo ctlptl:**

   ```bash
   ctlptl get clusters
   ```
</details>

---

## Instalar Tilt

<details>
  <summary>Sobre o Tilt</summary>

### O que é o Tilt?

O Tilt é uma ferramenta que agiliza o desenvolvimento em ambientes Kubernetes. Automatiza a construção, implantação e monitoramento do código, permitindo um ciclo de desenvolvimento mais rápido.

### Por que é necessário o Tilt?

No projeto **External Secrets Operator**, o Tilt é utilizado para desenvolver e testar alterações no código de forma eficiente, refletindo mudanças quase instantaneamente no ambiente Kubernetes local.

</details>

<details>
  <summary>Instalação do Tilt</summary>

### Versão Necessária
- **Pré-requisitos:** Instalar o Docker, kubectl, Kind e ctlptl.
- **Versão recomendada:** Versão mais recente disponível.

### Como Instalar o Tilt

<details>
  <summary>Instalação no Linux</summary>

1. **Baixar e executar o script de instalação:**

   ```bash
   curl -fsSL https://raw.githubusercontent.com/tilt-dev/tilt/master/scripts/install.sh | bash
   ```

2. **Verificar a instalação do Tilt:**

   ```bash
   tilt version
   ```

</details>

<details>
  <summary>Instalação no macOS</summary>

- **Usando o Homebrew:**

  ```bash
  brew install tilt-dev/tap/tilt
  ```

- **Verificar a instalação do Tilt:**

  ```bash
  tilt version
  ```

</details>

Para outras opções de instalação e mais detalhes, consulte o [guia oficial de instalação do Tilt](https://docs.tilt.dev/install.html).

</details>