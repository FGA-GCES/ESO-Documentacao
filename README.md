# GCES-ESO-Doc

## Repositório de Apoio para Contribuição ao External Secrets Operator

Este repositório foi criado com o objetivo de auxiliar alunos que estão contribuindo para o projeto External Secrets Operator (ESO). Aqui, você encontrará uma documentação completa com tutoriais que orientam como configurar o Kubernetes, o ESO e todos os pré-requisitos necessários para começar a trabalhar no projeto.

A documentação está organizada para fornecer uma base sólida, garantindo que você tenha todas as ferramentas e configurações adequadas para colaborar de forma eficiente no desenvolvimento e manutenção do External Secrets Operator.

## Apresentação das Tecnologias

### Golang

É uma linguagem de programação criada pelo Google, muito utilizada para desenvolvimento backend, de microserviços, aplicativos CLI, entre outros.

O Go é necessário no ESO para compilar, executar e contribuir com o código-fonte do projeto.

### Kubernetes

Kubernetes é um sistema de código aberto para automação de gerenciamento, escalonamento e implementação de contêiners.

Com o Kubernetes é possível orquestrar de forma mais fácil múltiplos contêineres com suporte à _auto healing_ (sobe novamente o contêiner quando este for derrubado), _work balance_ (distribui de forma dinâmica a carga de trabalho em vários ambientes de acordo com a necessidade), entre outros.

### External Secrets Operator (ESO)

O ESO é um operador Kubernetes que tem como função integrar secrets de sistemas externos, como o AWS Secrets Manager, HashiCorp Vault, etc. 

O objetivo do ESO é sincronizar secrets sensíveis de APIs externas com o Kubernetes, provendo uma maneira mais fácil e segura de lidar com os eles.

Imagine que você esteja lidando com dados sensíveis como um acesso ao banco de dados que esteja armazenado em um sistema externo. Com o ESO, esses dados são disponibilizados no Kubernetes como secrets, podendo ser consumidos pela aplicação. Além disso, caso as credenciais sejam atualizadas no AWS Secrets Manager, o ESO sincroniza as mudanças automaticamente com o Kubernetes.

## Estrutura do Repositório

As pastas deste repositório foram organizadas de forma a facilitar o processo de configuração e uso do External Secrets Operator (ESO), permitindo que você siga os passos necessários de maneira sequencial e eficiente. A estrutura está dividida da seguinte forma:

Setup: Contém os arquivos e instruções para a configuração inicial, incluindo a instalação do Kubernetes, ESO e demais pré-requisitos.
[SETUP](https://github.com/FGA-GCES/ESO-Documentacao/tree/main/docs/1-Setup)

Conectando: Orienta sobre como integrar o ESO ao Kubernetes e outras plataformas, incluindo como conectar com clusters kubernetes locais ou por meio de ferramentas de computação em nuvem como a AWS, Google cloud e Azure
[CONECTANDO](https://github.com/FGA-GCES/ESO-Documentacao/tree/main/docs/2-Conectando)

Links Externos: Uma coleção de recursos externos úteis, como artigos, fóruns e documentações oficiais, que podem auxiliar durante o desenvolvimento.
[LINKS](https://github.com/FGA-GCES/ESO-Documentacao/tree/main/docs/3-Links)

Seção com resolução de problemas encontrados durante o setup do projeto:
[COMMON_ISSUES](https://github.com/FGA-GCES/ESO-Documentacao/tree/main/docs/4-Common_issues)

## Executar a documentação localmente

A documentação foi desenvolvida usando a ferramenta mkdocs. Para visualiza-la localmente, é necessário ter o python3 instalado na máquina e seguir os passos abaixo:

(linux)

1. Criar ambiente virtual

```bash
python3 -m venv venv
```

2. Ativar ambiente virtual

```bash
source venv/bin/activate
```

3. Instalar as dependencias

```bash
pip install mkdocs mkdocs-material
```

4. Executar a doc no localhost:8000:

```bash
mkdocs serve
```
