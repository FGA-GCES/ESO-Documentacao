# Utilizando o External Secrets Operator com o Vault

Neste documento você aprenderá como utilizar o ESO (External Secrets Operator) em conjunto com
o [Vault](https://developer.hashicorp.com/vault/docs?product_intent=vault), o gerenciador de segredos da HashiCorp, em um cluster Kubernetes local configurado com
Kind.

## Criação do cluster

Para esse exemplo, utilizaremos um cluster Kubernetes local criado com o Kind. Com a seguinte configuração:

```yaml
apiVersion: kind.x-k8s.io/v1alpha4
kind: Cluster
nodes:
  - role: control-plane
  - role: worker
  - role: worker
```

Salve a configuração acima em um arquivo e execute o comando abaixo:

```sh
kind create cluster --config <arquivo>
```

## Adicionando Vault ao cluster

Podemos utilizar o Helm para instalar o Vault no cluster.

```sh
helm repo add hashicorp https://helm.releases.hashicorp.com
helm install vault hashicorp/vault
```

Para verificar os recursos criados, execute:

```sh
kubectl get all | grep vault
```

## Configurando o Vault

Antes de adicionar o ESO, é necessário configurar o Vault. Um maneira simples de realizar
esse processo é expondo a porta do `service/Vault`, utilizando o comando abaixo. Dessa forma, é possível
acessar sua interface web em: `http://localhost:8200`.

```sh
kubectl port-forward svc/vault --address 0.0.0.0 8200:8200
```

Preencha os campos **Key shares** e **Key threshold** com o valor 1 e clique em **Initialize**.

Salve a chave gerada e o initial token, pois serão necessárias para desbloquear o Vault. Clique em Continue.

Utilize a `key1` para desbloquear o Vault e o `root token` para logar.

## Engine de Segredos

Na interface web do Vault, clique em `Secrets Engines` na barra lateral e em seguida em `Enable new engine`.
Selecione a engine de segredos do tipo `Key/Value` KV e clique em **Enable engine**.

Com a engine habilitada, crique em `Create secret` e crie um segredo de chave `segredo1` com um valor arbitrário.
No campo de `Path` insira `tutorial/` e clique em **Save**.

## Adicionando o ESO ao cluster

Utilize o helm para instalar o ESO no cluster.

```sh
helm repo add external-secrets https://charts.external-secrets.io
helm install external-secrets \
   external-secrets/external-secrets \
    -n external-secrets \
    --create-namespace
```

Para verificar os recursos criados, execute:

```sh
kubectl -n external-secrets get all
```

## Criando um ClusterSecretStore

O ClusterSecretStore é responsável por armazenar as configurações de acesso ao Vault.
Para que ele tenha acesso ao Vault, é necessário criar um secret com o token de acesso.

```sh
kubectl create secret generic vault-policy-token --from-literal=token=<token>
```

Para criar o ClusterSecretStore, utilize o arquivo abaixo:
O atributo server precisa ser preenchido com o ClusterIP do Vault.
utilize o comando `kubectl get svc vault` para obter o ClusterIP.

```yaml
apiVersion: external-secrets.io/v1beta1
kind: ClusterSecretStore
metadata:
  name: vault-backend
spec:
  provider:
    vault:
      server: "http://<ClusterIP>:8200" # Endereço do ClusterIP 
      path: kv # Path do segredo criado no Vault
      version: "v2"
      auth:
        tokenSecretRef:
          name: "vault-policy-token" # Nome do secret que contém o token
          key: "token"               # Chave do token no secret
```

Para criar o recurso, salve a configuração em um arquivo e execute.

```sh
kubectl apply -f <arquivo>
```

## Criando um ExternalSecret

O ExternalSecret é responsável por criar a secret no cluster Kubernetes com o segredo do Vault.

```yaml
apiVersion: external-secrets.io/v1beta1
kind: ExternalSecret
metadata:
  name: external-secrets
spec:
  refreshInterval: 10s          # Intervalo de atualização do segredo
  secretStoreRef:
    name: vault-backend
    kind: ClusterSecretStore
  target:
    name: eso-secret            # Nome da secret que será criada
    creationPolicy: Owner
  data:
    - secretKey: segredo1       # Nome da chave do segredo
      remoteRef:
        key: kv/tutorial
        property: segredo1
```

Para criar o recurso, salve a configuração em um arquivo e execute.

```sh
kubectl apply -f <arquivo>
```

Após a criação do ExternalSecret, a secret pode ser verificada utilizando o comando:

```yaml
kubectl get secret
```

Para verificar o conteúdo da secret, utilize o comando:
```sh
kubectl get secret eso-secret -o yaml
```

copie o valor do atributo `data.segredo1` no yaml gerado e decodifique utilizando o comando:

```sh
echo "<valor-copiado>" | base64 -d
```

Atualize o segredo no Vault e verifique se a secret foi atualizada no cluster Kubernetes.
