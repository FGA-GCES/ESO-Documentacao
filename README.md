# GCES-ESO-Doc

## Repositório de Apoio para Contribuição ao External Secrets Operator

Este repositório foi criado com o objetivo de auxiliar alunos que estão contribuindo para o projeto External Secrets Operator (ESO). Aqui, você encontrará uma documentação completa com tutoriais que orientam como configurar o Kubernetes, o ESO e todos os pré-requisitos necessários para começar a trabalhar no projeto.

A documentação está organizada para fornecer uma base sólida, garantindo que você tenha todas as ferramentas e configurações adequadas para colaborar de forma eficiente no desenvolvimento e manutenção do External Secrets Operator.

## Apresentação das Tecnologias

### Golang

É uma linguagem de programação criada pelo Google, muito utilizada para desenvolvimento backend, de microserviços, aplicativos CLI, entre outros.

O Go é utilizado tanto no Kubernetes, quanto no ESO, as duas principais tecnologias envolvidas no trabalho.

### Kubernetes

Kubernetes é um sistema de código aberto para automação de gerenciamento, escalonamento e implementação de contêiners.

Com o Kubernetes é possível orquestrar de forma mais fácil múltiplos contêineres com suporte à _auto healing_ (sobe novamente o contêiner quando este for derrubado), _work balance_ (distribui de forma dinâmica a carga de trabalho em vários ambientes de acordo com a necessidade), entre outros.

### External Secrets Operator (ESO)

O ESO, é  uma ferramenta que integra segredos (variáveis sensíveis) de provedores externos, como AWS, Google Cloud, entre outros, com um ambiente kubertenes.

Com ele, é possível, pegar senhas salvas em um ambiente AWS, por exemplo, e subir para um contêiner em um cluster Kubernetes.

## Estrutura do Repositório

As pastas deste repositório foram organizadas de forma a facilitar o processo de configuração e uso do External Secrets Operator (ESO), permitindo que você siga os passos necessários de maneira sequencial e eficiente. A estrutura está dividida da seguinte forma:

Setup: Contém os arquivos e instruções para a configuração inicial, incluindo a instalação do Kubernetes, ESO e demais pré-requisitos.
[SETUP](https://github.com/frmiza/GCES-ESO-Doc/tree/docs/eso_docs/docs/1-Setup)

Conectando: Orienta sobre como integrar o ESO ao Kubernetes e outras plataformas, incluindo como conectar com clusters kubernets locais ou por meio de ferramentas de computação em nuvem como a AWS, Google cloud e Azure
[CONECTANDO](https://github.com/frmiza/GCES-ESO-Doc/tree/docs/eso_docs/docs/2-Conectando)

Links Externos: Uma coleção de recursos externos úteis, como artigos, fóruns e documentações oficiais, que podem auxiliar durante o desenvolvimento.
[LINKS](https://github.com/frmiza/GCES-ESO-Doc/tree/docs/eso_docs/docs/3-Links)

Seção com resolução de problemas encontrados durante o setup do projeto:
[COMMON_ISSUES](https://github.com/frmiza/GCES-ESO-Doc/tree/97a27e5594df9a12945dda4746d4dabacd47b30f/eso_docs/docs/4-Common_issues)

## Executar a documentação localmente

A documentação foi desenvolvida usando a ferramenta mkdocs. Para visualiza-la localmente, é necessário ter o python3 instalado na máquina e seguir os passos abaixo:

(linux)

1. Criar ambiente virtual

```bash
python3 -m venv docs
```

2. Ativar ambiente virtual

```bash
source docs/bin/activate
```

3. Instalar as dependencias

```bash
pip install mkdocs
pip install mkdocs-material
```

4. Executar a doc no localhost:8000:

```bash
cd eso_docs
mkdocs serve
```
