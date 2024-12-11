# Configurar o External Secrets Operator

Aqui será feita a configuração e utilização do ESO. Para conseguir acompanhar, é preciso ter seguido os passos de configuração inicial dos [pré requisitos](https://github.com/FGA-GCES/ESO-Documentacao/blob/main/docs/1-Setup/1-Pre_requisitos.md).

## Clonar o repositório

```bash
git clone https://github.com/external-secrets/external-secrets.git
cd external-secrets
```

## Instalar helm-unittest

Instalar helm-unittest para poder realizar testes automatizados no ESO.

```bash
helm plugin install https://github.com/helm-unittest/helm-unittest
```

# Build

## Importância dos comandos `make build` e `make docker.build` em um projeto Go

### Comandos

### **1. `make build`**
- **O que faz:**
  - Compila o código Go e gera o binário do projeto.

- **Importância:**
  - Facilita a construção do binário, executando os comandos necessários automaticamente.
  - Garante que o binário seja gerado de maneira consistente, seguindo as configurações definidas no `Makefile`.
  - Permite a verificação rápida de problemas de compilação e dependências.

---

### **2. `make docker.build IMAGE_NAME=external-secrets IMAGE_TAG=latest`**
- **O que faz:** 
  - Constrói uma imagem Docker do projeto utilizando o binário gerado no passo anterior.
  - A imagem é nomeada como `external-secrets` e marcada com a tag `latest` (ou outra tag especificada).

- **Importância:**
  - Empacota o binário Go e suas dependências em uma imagem Docker, tornando o projeto portátil e pronto para execução em qualquer ambiente que suporte Docker.
  - É essencial para projetos Kubernetes, como o **External Secrets Operator**, porque permite que o aplicativo seja distribuído e implantado como um contêiner.
  - Automatiza o processo de criação da imagem, reduzindo erros manuais e melhorando a eficiência no pipeline de CI/CD.

---

## Fluxo de Uso
1. Primeiro, construa o binário do projeto com o comando:
   ```bash
   make build
   ```
2. Após utilize o binario gerado para criar uma imagem docker:
    ```bash
    make docker.build IMAGE_NAME=external-secrets IMAGE_TAG=latest
    ```


# Testes

## Importância dos comandos `make test` e `make lint` em um projeto Go

### Comandos e Fluxo de Uso

### **1. Rodar testes**
```bash
make test
```

### O que faz:
- Executa os testes automatizados do projeto utilizando as ferramentas e configurações definidas no `Makefile`.

### Importância:
- Garante que as funcionalidades do projeto estão funcionando corretamente e que alterações no código não introduzem regressões.
- Automatiza a execução dos testes, tornando o processo rápido e consistente.
- Facilita a integração contínua (CI), permitindo detectar problemas antes de avançar para estágios posteriores no pipeline de desenvolvimento.


# Lint 
## Importância do comando `make lint` em um projeto Go
### O que faz:
- O comando `make lint` verifica a qualidade do código utilizando ferramentas de análise estática, como o `golangci-lint`.
- O comando com Docker executa o `golangci-lint` dentro de um contêiner, permitindo rodar o lint mesmo sem a ferramenta instalada localmente.

### Importância:
- Identifica problemas no estilo de codificação, possíveis bugs e más práticas antes mesmo de rodar ou testar o código.
- Melhora a legibilidade e a qualidade do código, alinhando-o aos padrões estabelecidos pela equipe ou pela comunidade Go.
- A versão com Docker garante que a ferramenta de linting será executada com as configurações corretas, mesmo que o ambiente local não tenha o `golangci-lint` instalado.

### Rodar lint no código:

```bash
make lint # OU
docker run --rm -v $(pwd):/app -w /app golangci/golangci-lint:v1.49.0 golangci-lint run
```

# Rodar a documentação:

```bash
make docs
```