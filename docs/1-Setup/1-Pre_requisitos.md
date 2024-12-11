## Qual o objetivo do External Secrets Operator ?

O objetivo do External Secrets Operator (ESO) é sincronizar chaves secretas de APIs externas com o Kubernetes. O ESO é uma coleção de recursos personalizados da API - ExternalSecret, SecretStore e ClusterSecretStore - que fornecem uma abstração amigável para o usuário da API externa, armazenando e gerenciando o ciclo de vida das chaves para você.

# Pré-requisitos

Para colaborar com o projeto [External Secrets Operator (ESO)](https://external-secrets.io/latest/), é necessário instalar algumas ferramentas no computador. Neste guia, será explicado o que é cada ferramenta, por que é necessária, a versão recomendada e como instalá-la no sistema operacional correspondente.

## Sistemas Operacionais Suportados

Para colaborar com o projeto **External Secrets Operator (ESO)**, é recomendado utilizar sistemas operacionais baseados em Unix, como **Linux** e **macOS**. O ambiente de desenvolvimento do ESO é principalmente voltado para esses sistemas, e muitas das ferramentas e scripts utilizados no desenvolvimento são projetados para funcionar neles.

### É possível desenvolver no Windows?

É possível utilizar o Windows para o desenvolvimento, mas há considerações importantes a serem feitas. Como o ambiente de desenvolvimento do ESO não é otimizado para o Windows, podem surgir pro   blemas de incompatibilidade com ferramentas como **Make**, **Tilt** e scripts shell. Os scripts de automação e comandos presentes no projeto são escritos para ambientes Unix, utilizando bash scripting, o que pode não ser compatível com o Windows sem adaptações. Este tutorial não cobrirá a instalação e configuração de ferramentas no Windows devido à complexidade e falta de testes.

---

## Instalar Go (Golang)

<details>
  <summary>Sobre o Golang</summary>
  <h3> O que é Go?</h3>
  <p> Go, também conhecido como Golang, é uma linguagem de programação criada pelo Google. É conhecida por ser eficiente, fácil de aprender e excelente para desenvolver aplicativos rápidos e escaláveis.</p>
  <h3> Por que é necessário Go?</h3>
  <p> No projeto <strong>External Secrets Operator</strong>, Go é utilizado para desenvolver partes fundamentais do código. É necessário para compilar, executar e contribuir com o código-fonte do projeto.</p>
</details>

<details>
  <summary>Instalação do Golang</summary>
  <h3> Versão Necessária</h3>
  <p><strong>Versão mínima:</strong> Go 1.20 ou superior.</p>
  <p><strong>Versão recomendada:</strong> Go 1.23.3</p>
  <blockquote> Durante o desenvolvimento deste guia, a versão mais recente do Go é a <strong>1.23.3</strong>, a qual funcionou perfeitamente com o projeto <strong>External Secrets Operator</strong>. Versões anteriores apresentaram falhas nos testes da aplicação. Antes de testar o projeto, verifique sua versão do Go.</blockquote>

  <h3> Como Instalar Go</h3>

  <details>
    <summary>Instalação no Linux</summary>
    <h3>1. Baixar o arquivo de instalação do Go:</h3>
    <p>Acesse o site oficial ou use o comando abaixo:</p>
    <pre><code>wget https://golang.org/dl/go1.23.3.linux-amd64.tar.gz</pre></code>
    <h3>2. Remover instalações anteriores do Go:</h3>
    <pre><code>sudo rm -rf /usr/local/go</pre></code>
    <h3>3. Extrair o novo arquivo do Go para `/usr/local`:</h3>
    <pre><code>sudo tar -C /usr/local -xzf go1.23.3.linux-amd64.tar.gz</pre></code>
    <h3>4. Atualizar o PATH adicionando `/usr/local/go/bin`:</h3>
    <p>Edite o arquivo `~/.profile` ou `/etc/profile` e adicione:</p>
    <pre><code>export PATH=$PATH:/usr/local/go/bin</pre></code>
    <p>Ou execute diretamente no terminal para a sessão atual:</p>
    <pre><code>export PATH=$PATH:/usr/local/go/bin</pre></code>
    <h3>5. Aplicar as alterações do PATH imediatamente:</h3>
    <pre><code>source ~/.profile</pre></code>
    <h3>6. Verificar a instalação do Go e se está na versão suportada:</h3>
    <pre><code>go version</pre></code>
    <blockquote><strong>Nota:</strong> Para Debian/Ubuntu, é possível instalar o Go utilizando o Snap:
    <pre><code>sudo snap install --classic go</pre></code></blockquote>
  </details>

<details>
  <summary>Instalação no macOS</summary>
  <h3>1. Baixar o arquivo de instalação do Go:</h3>
  <a href="https://go.dev/dl/go1.23.3.darwin-arm64.pkg">Apple macOS (ARM64), macOS 11 ou superior</a>
  <a href="https://go.dev/dl/go1.23.3.darwin-amd64.pkg">Apple macOS (Intel), macOS 10.15 ou superior</a>
  <h3>2. Executar o arquivo baixado e seguir as instruções de instalação.</h3>
  <p>O pacote instala a distribuição do Go em `/usr/local/go`. O instalador deve adicionar o diretório `/usr/local/go/bin` à variável de ambiente `PATH`. Pode ser necessário reiniciar qualquer sessão aberta do Terminal para que a alteração entre em vigor.</p>
  <h3>3. Verificar a instalação do Go e se está na versão suportada:</h3>
  <pre><code>go version</pre></code>
</details>

<p>Quaisquer dúvidas ou problemas com a instalação do Go, consulte a <a href="https://go.dev/doc/install">documentação oficial</a>.</p>

</details>

## Instalar Helm

<details>
  <summary>Sobre o Helm</summary>
  <h3>O que é o Helm?</h3>
  <p>O Helm é um gerenciador de pacotes para Kubernetes, a plataforma que automatiza a implantação, escalonamento e gerenciamento de aplicativos em contêineres.</p>
  
  <h3>Por que é necessário o Helm?</h3>
  <p>No projeto <strong>External Secrets Operator</strong>, o Helm é utilizado para simplificar a instalação e gerenciamento de aplicações dentro do Kubernetes, automatizando processos complexos de configuração e implantação.</p>
</details>

<details>
  <summary>Instalação do Helm</summary>
  <h3>Versão Necessária</h3>
  <p><strong>Versão recomendada:</strong> Helm 3 (versão mais recente do Helm 3).</p>
  <h3>Como Instalar o Helm</h3>

  <details>
    <summary>Instalação no Linux</summary>
    <h3>1. Baixar o script de instalação:</h3>
    <pre><code>curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3</code></pre>
    <h3>2. Tornar o script executável:</h3>
    <pre><code>chmod 700 get_helm.sh</code></pre>
    <h3>3. Executar o script de instalação:</h3>
    <pre><code>./get_helm.sh</code></pre>
    <h3>4. Verificar a instalação do Helm:</h3>
    <pre><code>helm version</code></pre>
  </details>

  <details>
    <summary>Instalação no macOS</summary>
    <h3>1. Usando o Homebrew:</h3>
    <pre><code>brew install helm</code></pre>
    <h3>2. Verificar a instalação do Helm:</h3>
    <pre><code>helm version</code></pre>
  </details>

  <p>Para outras opções de instalação e mais detalhes, consulte o <a href="https://helm.sh/docs/intro/install/">guia oficial de instalação do Helm</a>.</p>
</details>

---

## Instalar yq

<details>
  <summary>Sobre o yq</summary>
  <h3>O que é o yq?</h3>
  <p>O yq é uma ferramenta de linha de comando para ler, manipular e escrever arquivos YAML, amplamente utilizados para configurações.</p>
  
  <h3>Por que é necessário o yq?</h3>
  <p>No projeto <strong>External Secrets Operator</strong>, o yq é utilizado para automatizar a edição de arquivos de configuração YAML, facilitando ajustes e implementações.</p>
</details>

<details>
  <summary>Instalação do yq</summary>
  <h3>Versão Necessária</h3>
  <p><strong>Versão recomendada:</strong> yq v4.44.3 ou superior.</p>

  <h3>Como Instalar o yq</h3>

  <details>
    <summary>Instalação no Linux</summary>
    <h3>1. Baixar o binário do yq:</h3>
    <pre><code>wget https://github.com/mikefarah/yq/releases/download/v4.44.3/yq_linux_amd64.tar.gz</code></pre>
    <h3>2. Extrair o arquivo baixado:</h3>
    <pre><code>tar xvf yq_linux_amd64.tar.gz</code></pre>
    <h3>3. Mover o binário para <code>/usr/local/bin</code> e tornar executável:</h3>
    <pre><code>sudo mv yq_linux_amd64 /usr/local/bin/yq</code></pre>
    <pre><code>sudo chmod +x /usr/local/bin/yq</code></pre>
    <h3>4. Verificar a instalação do yq:</h3>
    <pre><code>yq --version</code></pre>
    <blockquote>
      <strong>Alternativa:</strong> Caso encontre problemas, instale via Snap:
      <pre><code>sudo snap install yq</code></pre>
    </blockquote>
  </details>

  <details>
    <summary>Instalação no macOS</summary>
    <h3>1. Usando o Homebrew:</h3>
    <pre><code>brew install yq</code></pre>
    <h3>2. Verificar a instalação do yq:</h3>
    <pre><code>yq --version</code></pre>
  </details>

  <p>Para outras opções de instalação e mais detalhes, consulte o <a href="https://github.com/mikefarah/yq">repositório oficial do yq</a>.</p>
</details>

---

## Instalar jq

<details>
  <summary>Sobre o jq</summary>
  <h3>O que é o jq?</h3>
  <p>O jq é uma ferramenta de linha de comando para processar e manipular dados em formato JSON.</p>
  
  <h3>Por que é necessário o jq?</h3>
  <p>No projeto <strong>External Secrets Operator</strong>, o jq é essencial para trabalhar com dados JSON, permitindo filtrar e transformar informações de forma eficiente.</p>
</details>

<details>
  <summary>Instalação do jq</summary>
  <h3>Versão Necessária</h3>
  <p><strong>Versão recomendada:</strong> jq 1.6 ou superior.</p>

  <h3>Como Instalar o jq</h3>

  <details>
    <summary>Instalação no Linux</summary>
    <h3>1. Para Debian/Ubuntu:</h3>
    <pre><code>sudo apt-get install jq</code></pre>
    <h3>2. Para Fedora:</h3>
    <pre><code>sudo dnf install jq</code></pre>
    <h3>3. Verificar a instalação do jq:</h3>
    <pre><code>jq --version</code></pre>
  </details>

  <details>
    <summary>Instalação no macOS</summary>
    <h3>1. Usando o Homebrew:</h3>
    <pre><code>brew install jq</code></pre>
    <h3>2. Verificar a instalação do jq:</h3>
    <pre><code>jq --version</code></pre>
  </details>

  <p>Para outras opções de instalação e mais detalhes, consulte o <a href="https://stedolan.github.io/jq/">site oficial do jq</a>.</p>
</details>


---

## Instalar Docker

<details>
  <summary>Sobre o Docker</summary>
  <h3>O que é o Docker?</h3>
  <p>O Docker é uma plataforma que permite criar, implantar e executar aplicativos em contêineres. Os contêineres permitem empacotar uma aplicação com todas as suas dependências em uma unidade padrão para desenvolvimento e implantação.</p>
  
  <h3>Por que é necessário o Docker?</h3>
  <p>No projeto <strong>External Secrets Operator</strong>, o Docker é usado para criar imagens de contêineres e executar serviços em ambientes isolados. É essencial para o desenvolvimento, teste e implantação da aplicação dentro de um ambiente Kubernetes.</p>
</details>

<details>
  <summary>Instalação do Docker</summary>
  <h3>Como Instalar o Docker</h3>

  <details>
    <summary>Instalação no Linux</summary>
    <h3>1. Atualizar os pacotes existentes:</h3>
    <pre><code>sudo apt-get update</code></pre>
    <h3>2. Instalar pacotes necessários:</h3>
    <code>sudo apt-get install \
                ca-certificates \
                curl \
                gnupg \
                lsb-release</code>
    <h3>3. Adicionar a chave GPG oficial do Docker:</h3>
    <pre><code>curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg</code></pre>
    <h3>4. Adicionar o repositório do Docker:</h3>
    <pre><code>echo \
"deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] \
https://download.docker.com/linux/ubuntu \
$(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
</code></pre>
    <h3>5. Instalar o Docker Engine:</h3>
    <pre><code>sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io</code></pre>
    <h3>6. Verificar a instalação do Docker:</h3>
    <pre><code>sudo docker run hello-world</code></pre>
  </details>

  <details>
    <summary>Instalação no macOS</summary>
    <h3>1. Baixar o Docker Desktop para macOS:</h3>
    <p>Acesse o site oficial e baixe o Docker Desktop:</p>
    <ul>
      <li><a href="https://desktop.docker.com/mac/stable/amd64/Docker.dmg">Docker Desktop para Mac com Intel Chip</a></li>
      <li><a href="https://desktop.docker.com/mac/stable/arm64/Docker.dmg">Docker Desktop para Mac com Apple Chip (M1)</a></li>
    </ul>
    <h3>2. Instalar o Docker Desktop:</h3>
    <ol>
      <li>Abra o arquivo <code>Docker.dmg</code>.</li>
      <li>Arraste o ícone do Docker para a pasta <code>Applications</code>.</li>
      <li>Inicie o Docker Desktop a partir da pasta <code>Applications</code>.</li>
    </ol>
    <h3>3. Verificar a instalação do Docker:</h3>
    <pre><code>docker --version</code></pre>
  </details>

  <p>Para outras opções de instalação e mais detalhes, consulte a <a href="https://docs.docker.com/get-docker/">documentação oficial do Docker</a>.</p>
</details>

<details>
  <summary>Configuração necessária no Docker</summary>
  <h3>Configurar Docker para Uso sem Root</h3>
  <p>Por padrão, o Docker requer privilégios de superusuário (root) para executar. Para facilitar o uso, é recomendado adicionar o usuário atual ao grupo <code>docker</code> para executar comandos sem <code>sudo</code>.</p>

  <details>
    <summary>Passos para configurar o Docker sem root no Linux</summary>
    <h3>1. Criar o grupo docker (se não existir):</h3>
    <pre><code>sudo groupadd docker</code></pre>
    <h3>2. Adicionar o usuário atual ao grupo docker:</h3>
    <pre><code>sudo usermod -aG docker $USER</code></pre>
    <h3>3. Aplicar as alterações de grupo sem fazer logout:</h3>
    <pre><code>newgrp docker</code></pre>
    <h3>4. Verificar se é possível executar o Docker sem sudo:</h3>
    <pre><code>docker run hello-world</code></pre>
    <p>Se o comando funcionar sem erros, a configuração foi bem-sucedida.</p>
  </details>
</details>

---

## Instalar kubectl

<details>
  <summary>Sobre o kubectl</summary>
  <h3>O que é o kubectl?</h3>
  <p>O <strong>kubectl</strong> é a ferramenta de linha de comando para gerenciar clusters Kubernetes. Permite executar comandos no cluster, gerenciar recursos e depurar aplicações.</p>
  <h3>Por que é necessário o kubectl?</h3>
  <p>No projeto <strong>External Secrets Operator</strong>, o kubectl é usado para interagir com o cluster Kubernetes local ou remoto, aplicar configurações e verificar o estado dos recursos implantados.</p>
</details>

<details>
  <summary>Instalação do kubectl</summary>
  <h3>Versão Necessária</h3>
  <p><strong>Versão compatível com a versão do Kubernetes instalada (geralmente a versão estável mais recente).</strong></p>
  <h3>Como Instalar o kubectl</h3>
  <details>
    <summary>Instalação no Linux</summary>
    <h3>1. Baixar a versão mais recente do kubectl:</h3>
    <pre><code>curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"</code></pre>
    <h3>2. Tornar o binário executável:</h3>
    <pre><code>chmod +x kubectl</code></pre>
    <h3>3. Mover o binário para o PATH:</h3>
    <pre><code>sudo mv kubectl /usr/local/bin/</code></pre>
    <h3>4. Verificar a instalação do kubectl:</h3>
    <pre><code>kubectl version --client</code></pre>
  </details>

  <details>
    <summary>Instalação no macOS</summary>
    <h3>1. Usando o Homebrew:</h3>
    <pre><code>brew install kubectl</code></pre>
    <h3>2. Verificar a instalação do kubectl:</h3>
    <pre><code>kubectl version --client</code></pre>
  </details>

  <p>Para outras opções de instalação e mais detalhes, consulte a <a href="https://kubernetes.io/docs/tasks/tools/">documentação oficial do kubectl</a>.</p>
</details>

---

## Instalar ctlptl e criar um cluster Kind com registro local

<details>
  <summary>Sobre o ctlptl</summary>
  <h3>O que é o ctlptl?</h3>
  <p>O <strong>ctlptl</strong> (Control Plane Tool) é uma ferramenta para gerenciar clusters locais de desenvolvimento Kubernetes. Ele facilita a criação e gerenciamento de clusters como o <strong>Kind</strong> (Kubernetes in Docker) e a configuração de registros locais de contêiner.</p>
  <h3>Por que é necessário o ctlptl?</h3>
  <p>No projeto <strong>External Secrets Operator</strong>, o ctlptl é usado para criar e gerenciar um cluster Kubernetes local usando o Kind, além de configurar um registro local de contêiner para armazenar imagens Docker durante o desenvolvimento.</p>
</details>

<details>
  <summary>Instalação do ctlptl</summary>
  <h3>Versão Necessária</h3>
  <p><strong>Versão mais recente disponível do ctlptl.</strong></p>

  <h3>Como Instalar o ctlptl</h3>

 <details>
  <summary>Instalação no Linux</summary>
  <h3>1. Instalar o ctlptl:</h3>
  <p>Use o comando abaixo para instalar a versão <code>0.8.36</code> do ctlptl diretamente em <code>/usr/local/bin</code>. Substitua <code>0.8.36</code> por outra versão, se necessário.</p>
  <pre><code>
CTLPTL_VERSION="0.8.36"
curl -fsSL https://github.com/tilt-dev/ctlptl/releases/download/v$CTLPTL_VERSION/ctlptl.$CTLPTL_VERSION.linux.x86_64.tar.gz | sudo tar -xzv -C /usr/local/bin ctlptl
  </code></pre>
  
  <h3>2. Verificar a instalação do ctlptl:</h3>
  <pre><code>
ctlptl version
  </code></pre>
</details>

<details>
  <summary>Instalação via Go</summary>
  <h3>1. Certifique-se de que o Go está instalado:</h3>
  <p>Se o Go não estiver instalado, siga as instruções no <a href="https://go.dev/doc/install">site oficial do Go</a>.</p>
  
  <h3>2. Instale o ctlptl via Go:</h3>
  <pre><code>
go install github.com/tilt-dev/ctlptl/cmd/ctlptl@latest
  </code></pre>

  <h3>3. Adicione o diretório <code>$GOPATH/bin</code> ao PATH (se necessário):</h3>
  <pre><code>
export PATH=$PATH:$(go env GOPATH)/bin
  </code></pre>
  
  <h3>4. Verifique a instalação do ctlptl:</h3>
  <pre><code>
ctlptl version
  </code></pre>
</details>

  <details>
    <summary>Instalação no macOS</summary>
    <h3>1. Usando o Homebrew:</h3>
    <pre><code>brew install tilt-dev/tap/ctlptl</code></pre>
    <h3>2. Verificar a instalação do ctlptl:</h3>
    <pre><code>ctlptl version</code></pre>
  </details>
</details>

<h3>Criar um Cluster Kind com Registro Local</h3>

<details>
  <summary>Sobre o Kind</summary>
  <p>O <strong>Kind</strong> (Kubernetes in Docker) é uma ferramenta para executar clusters Kubernetes locais usando contêineres Docker como nós do cluster.</p>
</details>

<details>
  <summary>Como Criar um Cluster Kind com Registro Local</summary>
  <h3>1. Criar um registro local de contêiner:</h3>
  <pre><code>docker run -d --restart=always -p "5000:5000" --name kind-registry registry:2</code></pre>
  <h3>2. Criar um cluster Kind usando o ctlptl e conectá-lo ao registro local:</h3>
  <pre><code>ctlptl create cluster kind --registry=kind-registry</code></pre>
  <p>Isso criará um cluster Kind configurado para usar o registro local em <code>localhost:5000</code>.</p>
  <h3>3. Verificar se o cluster está funcionando:</h3>
  <pre><code>kubectl cluster-info --context kind-kind</code></pre>
  <h3>4. Listar os clusters gerenciados pelo ctlptl:</h3>
  <pre><code>ctlptl get clusters</code></pre>
</details>

---

## Instalar Tilt

<details>
  <summary>Sobre o Tilt</summary>
  <h3>O que é o Tilt?</h3>
  <p>O Tilt é uma ferramenta que agiliza o desenvolvimento em ambientes Kubernetes. Automatiza a construção, implantação e monitoramento do código, permitindo um ciclo de desenvolvimento mais rápido.</p>
  <h3>Por que é necessário o Tilt?</h3>
  <p>No projeto <strong>External Secrets Operator</strong>, o Tilt é utilizado para desenvolver e testar alterações no código de forma eficiente, refletindo mudanças quase instantaneamente no ambiente Kubernetes local.</p>
</details>

<details>
  <summary>Instalação do Tilt</summary>
  <h3>Versão Necessária</h3>
  <ul>
    <li><strong>Pré-requisitos:</strong> Instalar o Docker, kubectl, Kind e ctlptl.</li>
    <li><strong>Versão recomendada:</strong> Versão mais recente disponível.</li>
  </ul>

  <h3>Como Instalar o Tilt</h3>

  <details>
    <summary>Instalação no Linux</summary>
    <h3>1. Baixar e executar o script de instalação:</h3>
    <pre><code>curl -fsSL https://raw.githubusercontent.com/tilt-dev/tilt/master/scripts/install.sh | bash</code></pre>
    <h3>2. Verificar a instalação do Tilt:</h3>
    <pre><code>tilt version</code></pre>
  </details>

  <details>
    <summary>Instalação no macOS</summary>
    <h3>1. Usando o Homebrew:</h3>
    <pre><code>brew install tilt-dev/tap/tilt</code></pre>
    <h3>2. Verificar a instalação do Tilt:</h3>
    <pre><code>tilt version</code></pre>
  </details>

  <p>Para outras opções de instalação e mais detalhes, consulte o <a href="https://docs.tilt.dev/install.html">guia oficial de instalação do Tilt</a>.</p>
</details>