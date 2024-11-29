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

## Build e teste

- Para rodar utilize o make:

```bash
make build
make docker.build IMAGE_NAME=external-secrets IMAGE_TAG=latest
```

- Rodar testes:

```bash
make test
```

- fazer lint no código:

```bash
make lint # OU
docker run --rm -v $(pwd):/app -w /app golangci/golangci-lint:v1.49.0 golangci-lint run
```

- Rodar a documentação:

```bash
make docs
```