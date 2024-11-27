# Problemas enquanto executa "make docker.build IMAGE_NAME=external-secrets IMAGE_TAG=latest"

## Problema 1:

### ERRO:
    test -s /home/meu-user/Área de Trabalho/GCES/external-secrets/bin/tilt || curl -fsSL https://github.com/tilt-dev/tilt/releases/download/v0.33.10/tilt.0.33.10.linux.x86_64.tar.gz | tar -xz -C /home/meu-user/Área de Trabalho/GCES/external-secrets/bin tilt
    /bin/bash: linha 1: test: número excessivo de argumentos
    tar: de: Não foi encontrado no arquivo-tar
    tar: Trabalho/GCES/external-secrets/bin: Não foi encontrado no arquivo-tar
    tar: Saindo com status de falha em razão de erros anteriores
    make: *** [Makefile:355: de] Erro 2


### Solução e explicação:
Esse "número excessivo de argumentos" era sobre literalmente o nome do diretório "Área de Trabalho". A solução felizmente foi fácil: Colocar a pasta, nesta caso "GCES" em outro diretório como "Documentos" por exemplo. Depois que organizar isso, tente novamente rodar "make docker.build IMAGE_NAME=external-secrets IMAGE_TAG=latest" na pasta do external-secrets no novo diretório.

---

## Problema 2:

### ERRO:
    ./hack/crd.generate.sh: linha 19: jq: comando não encontrado
    make: *** [Makefile:136: generate] Erro 127


### Solução e explicação:
Esse erro aconteceu antes da documentação desse repositório estar atualizada, então é improvável que ele volte a acontecer. Se você é sortudo e aconteceu com você, esse comando resolve rapidinho. Depois que ele executar, tente novamente rodar "make docker.build IMAGE_NAME=external-secrets IMAGE_TAG=latest" na pasta do external-secrets.

    sudo apt install jq 