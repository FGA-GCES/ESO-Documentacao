# Problema com yq e jq no setup do projeto 

Esse documento tem o objetivo de expor um problema encontrado durante o setup do projeto relacionado às bibliotecas yq e jq no linux.

## Contexto

O problema foi identificado já no inicio do setup do projeto, durante uma tentativa de execução do comando:

```bash
make build 
```

### Pré-requisitos

Ao executar o comando `make build` dentro da raiz do projeto do ESO, é necessária a utilização de uma biblioteca chamada `yq` que realiza processamento de arquivos com extensão YAML, XML ou TOML e trabalha em conjunto com o `jq` para extrair e trabalhar com campos específicos de um arquivo convertido pra objeto (JSON) pelo `yq`.

Na documentação oficial do ESO, consta que de fato é necessário possuir instalada na máquina a biblioteca `yq` com versão igual ou superior a 4.2X.X.

![yq required version](https://raw.githubusercontent.com/frmiza/GCES-ESO-Doc/97a27e5594df9a12945dda4746d4dabacd47b30f/eso_docs/assets/pictures/ESO_make_issue_2.png)

No entanto vale ressaltar que para que o yq funcione corretamente é obrigatório se ter instalada também sua dependência, o jq.
As instruções de instalação de cada um podem ser acessadas nos respectivos links:

- [yq installation](https://kislyuk.github.io/yq/#synopsis)
- [jq installation](https://jqlang.github.io/jq/download/)

As configurações do ambiente no qual o problema foi identificado são:

|Parâmetro|Valor|Versão|
|---------|-----|------|
|Sistema operacional|Debian GNU/Linux 12 (bookworm) x86_64|12|
|Golang|go1.23.0 linux/amd64|1.23.0|
|yq|yq version 4.2.0|4.2.0|
|jq|jq-1.6|1.6|

### Descrição do problema

Ao executar o `make build`, é retornado o seguinte erro no std output:

![erro no terminal](https://raw.githubusercontent.com/frmiza/GCES-ESO-Doc/97a27e5594df9a12945dda4746d4dabacd47b30f/eso_docs/assets/pictures/ESO_make_issue_3.png)

O projeto não é montado como deveria, e essa mensagem é exibida no terminal, seguida do trecho de help do manual do yq.

## Possíveis causas e troubleshooting

#### Incompatibilidade de versão

Estimamos que uma das causas do problema possa estar relacionado a problemas de versão entre as ferramentas que o make utiliza para montar o projeto. 

Recomendamos que ao se deparar com esse problema, **verifique as versões de cada uma dessas duas ferramentas no seu sistema** e se estão de acordo com o pedido pelo ESO, e ainda **se o próprio jq está instalado** por se tratar de uma dependência auxiliar que pode não vir por padrão no seu sistema.

Abaixo estão alguns fluxos de troubleshooting que podem ajudar:

#### Versão inconsistente

Nas primeiras tentativas também foi identificado um problema em que o yq mostrava versão 0.0.0, para isso bastou desinstalar o yq com o gerenciador de pacotes padrão do debian (apt) com o comando 

```bash
sudo apt remove yq
sudo apt autoremove # remove dependencias que nao sao mais utilizadas
```

#### Executáveis conflitantes  

OBS2: Verificar também se mesmo removendo o yq, alguma versão conflitante não permanece no sistema. Caso o pacote já tenha sido removido via apt/snap/flatpak, e o comando `yq --version` ainda retorne uma versão válida, o binário que está sendo executado pode ser encontrado e removido com os seguintes comandos:

```bash
sudo which yq
sudo rm /path/to/bin/yq # Esse deve ser o path retornado pelo comando which
```

#### Instalar versões alternativas ao package manager da distribuição linux

A solução que melhor funcionou para resolver essa etapa do setup, foi a de instalar essas ferramentas por meios alternativos ao apt. Para isso **primeiro é importante remover as duas ferramentas do sistema** para garantir uma instalação "limpa".

##### instalando yq mais atualizado

A versão mais atualizada encontrada foi diretamente no binários disponibilizado nessa página do [github do yq](https://github.com/mikefarah/yq/#install)

Pode ser instalada com: 

```bash
sudo wget https://github.com/mikefarah/yq/releases/latest/download/yq_linux_amd64 -O /usr/bin/yq && sudo chmod +x /usr/bin/yq 
```

O sudo é necessário pois está sendo adicionado o binário direto no diretório padrão (que geralmente já está no $PATH) do sistema para executáveis. Caso deseje, pode alterar o path de download e:

1. Adicionar manualmente o diretório escolhido ao $PATH, ou
2. Criar um "alias" no .bashrc do seu sistema com o valor do path para o binário.

O resultado após essa instalação é: 

![yq version](https://raw.githubusercontent.com/frmiza/GCES-ESO-Doc/97a27e5594df9a12945dda4746d4dabacd47b30f/eso_docs/assets/pictures/ESO_make_issue_4.png)

##### instalando jq mais atualizado

A versão mais atualizada do binário do jq pode ser baixada através do link na [documentação de instalação jq](https://jqlang.github.io/jq/download/)

Para o caso desse projeto, a versão escolhida foi a 1.7.1 AMD64.

![bin jq](https://raw.githubusercontent.com/frmiza/GCES-ESO-Doc/97a27e5594df9a12945dda4746d4dabacd47b30f/eso_docs/assets/pictures/ESO_make_issue_5.png)

Ao clicar no link um binário do jq será baixado para o diretório de Downloads definido no seu navegador. Para garantir que o binário será encontrado durante a execução make, siga os passos a seguir:

1. Abra o terminal e navegue até o path de download do binário
2. Adicione a permissão de execução do binário com o seguinte comando: 
```bash
sudo chmod +x nome_do_arquivo # substitua pelo nome do seu arquivo, no nosso caso o arquivo chamava-se jq-linux-amd64
```
3. Navegue para o seu diretório Home: `$ cd ~`
4. Abra o arquivo oculto `.bashrc` (caso não exista, crie-o com `touch .bashrc`)
5. Adicione ao final do arquivo o seguinte alias:
```bash
alias jq="/path/para/o/seu/binario_jq" # Substitua pelo path onde está o executável baixado
```
6. Após salvar e fechar o arquivo, basta abrir um novo terminal e verificar que o jq está acessível:

![jq version](https://raw.githubusercontent.com/frmiza/GCES-ESO-Doc/97a27e5594df9a12945dda4746d4dabacd47b30f/eso_docs/assets/pictures/ESO_make_issue_6.png)

OBS: Para esse tutorial foi usado o bash, caso esteja utilizando um shell diferente, busque adaptar os comandos e arquivos de configuração quando necessário

OBS2: Uma alternativa à criação do alias, é adicionar o path do binário (após a execução do chmod +x) à variável $PATH. Para isso pode ser editado/criado o arquivo .profile na sua home.

## Verificando a solução

Após instaladas as versões anteriores do jq e yq, o comando make build foi executado corretamente:

##### Versões e execução do make build

![make1](https://raw.githubusercontent.com/frmiza/GCES-ESO-Doc/97a27e5594df9a12945dda4746d4dabacd47b30f/eso_docs/assets/pictures/ESO_make_issue_7.png)

São instaladas algumas dependencias do GO...

E o resultado:

![make1](https://raw.githubusercontent.com/frmiza/GCES-ESO-Doc/97a27e5594df9a12945dda4746d4dabacd47b30f/eso_docs/assets/pictures/ESO_make_issue_8.png)