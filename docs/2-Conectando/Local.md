# Conexão ESO local

Aqui será mostrado como criar um POD e fazer a conexão com o ESO. Para fazer testes mais complexos e específicos crie o seu própio cluster Kubernet.

## Configurar um POD básico

### Ver pods existentes no namespace "default"

Para executar o comando abaixo, é necessário estar no mesmo repositório onde o seu kubeconfig está. Após fazer essa verificação, execute o comando:

```bash
kubectl get pods --namespace default --kubeconfig kubeconfig
```
O comando é usado para listar todos os pods no namespace "default" de um cluster Kubernetes. A opção --kubeconfig kubeconfig especifica o arquivo de configuração a ser usado para se conectar ao cluster.

### Criar o Pod definido no arquivo `pod.yaml`

Para executar o comando abaixo, certifique-se de que o caminho para o arquivo `pod.yml` especificado no comando está correto.

```bash
kubectl apply -f ../parte01/pod.yaml --namespace default --kubeconfig kubeconfig
```
O comando cria ou atualiza os recursos definidos no arquivo `pod.yml`  no namespace default, utilizando o arquivo de configuração kubeconfig para se conectar ao cluster.

### Testar acesso ao Postgres

Fazer "port forwarding" para ver se o Postgres está funcionando. Port forwarding é ótimo para debugar aplicações.

```bash
kubectl port-forward pod/exemplo-postgres 5432:5432 --namespace default --kubeconfig kubeconfig
```

Acessar Postgres usando `psql` (também é possível usar `pgadmin`, `dbeaver` e outras ferramentas).

```bash
psql --host localhost --port 5432 --username postgres postgres
```


## Rodando o ESO

Para rodar o ESO será utilizado o tilt, a forma mais simples de se fazer a conexão e verificar as modificações feitas no código.

Para rodar, vá para a raiz do arquivo em que o repositório foi clonado, e utilize o seguinte comando com o POD subido:

```bash
make tilt-up
```

## Deletar o Pod criado anteriormente

Para finalizar o POD rode:

```bash
kubectl delete pod/exemplo-postgres --namespace default --kubeconfig kubeconfig
```