# Glossário de Tecnologias Relacionadas ao ESO.
Está organizado em ordem alfabética!



### **Clusters**

---

### **Developments**
- **O que é?**  
  Nesse contexto, é uma forma de se fazer um conjunto de Pods. Isso ainda dentro de um Nó.

---

### **Docker**

---

### **ESO - External Secrets Operator**

---

### **Go**

---

### **Helm**
- **O que é?**  
  Um gerenciador de pacotes para Kubernetes que facilita a implantação e o gerenciamento de aplicações usando templates chamados "charts".
- **Para que serve?**  
  Simplifica a configuração, instalação e atualização de aplicativos no Kubernetes.
- **Links úteis:**  
  - [Documentação oficial](https://helm.sh/docs/)
  - [GitHub do projeto](https://github.com/helm/helm)

---
### **HPA**
- **O que é?**  
 Horizontal Pod Autoscaler (HPA)
- **Para que serve?**  
  É usado para controlar a quantidade de Pods que há em um Deployment. Por exemplo, se o uso de CPU estiver muito alto, o HPA aumentaria a quantidade de pods. Também é possível utilizar o Vertical Pod Autoscaler (VPA), que aumentaria a quantidade de recursos de cada pod em vez de aumentar a quantidade de Pod.
  
  Fonte:  [Leo Michalski](https://github.com/leomichalski/kubernetes-para-devs/blob/main/README.md)

---

### **Ingress**
- **O que é?**  
  Em um cluster Kubernetes no qual todas as requisições chegam no mesmo IP e na mesma porta, os Ingresses são responsáveis por direcionar (de acordo com o DNS e o endpoint de cada requisição) essas requisições para os Services adequados. Também pode ser usado para outras finalidades.
  
   Fonte:  [Leo Michalski](https://github.com/leomichalski/kubernetes-para-devs/blob/main/README.md)

- **Para que serve?**  
  Oferece um ponto de entrada único para rotear tráfego para serviços internos.
- **Links úteis:**  
  - [Sobre Ingress](https://kubernetes.io/docs/concepts/services-networking/ingress/)

---

### **Issuer**
- **O que é?**  
  Um componente em ferramentas como o Cert-Manager para emitir certificados.
- **Para que serve?**  
  Gerencia a emissão de certificados TLS automáticos para serviços em Kubernetes.Ele que emite o certificado SSL para os Ingresses poderem criptografar (com HTTPS) as requisições que entram e saem, por exemplo.

- **Links úteis:**  
  - [Documentação do Cert-Manager](https://cert-manager.io/docs/)

---

### **Kind**

---

### **Kubectl**

---

### **Kubernetes**
- **O que é?**  
  Uma plataforma de orquestração de contêineres que automatiza a implantação, escala e gerenciamento de aplicativos. É Open Source.
- **Para que serve?**  
  Garante alta disponibilidade, escalabilidade e monitoramento de aplicações em contêineres.
- **Links úteis:**  
  - [Documentação oficial](https://kubernetes.io/docs/)
  - [GitHub do projeto](https://github.com/kubernetes/kubernetes)

---

### **Nginx**

--- 


### **Lint**

---

### **Pods**
- **O que é?**  
  A menor unidade de computação em Kubernetes, que agrupa um ou mais contêineres.
- **Para que serve?**  
  Gerencia contêineres que compartilham recursos e atuam como uma única entidade em um cluster.
- **Links úteis:**  
  - [Sobre Pods](https://kubernetes.io/docs/concepts/workloads/pods/)


<center>

<figure markdown>
<font size="3"><p style="text-align: center"><b>Imagem 2</b> - Organização dos Pods em um cluster</p></font>

![pods](/assets/pictures/Glossario1.png)

<font size="3"><p style="text-align: center">Fonte: [Armosec blog](https://www.armosec.io/blog/kubernetes-security-best-practices//)</p></font>

</figure>

</center>

---

### **Secrets**
- **O que é?**  
São os dados sensíveis que queremos armazenar, gerenciar e utilizar usando o ESO.

---

### **Tilt**
- **O que é?**  
  Uma ferramenta que ajuda no desenvolvimento local para Kubernetes, permitindo visualizar e gerenciar rapidamente alterações em aplicativos.
- **Para que serve?**  
  Facilita o fluxo de desenvolvimento em Kubernetes, atualizando o estado do cluster automaticamente com base nas mudanças no código. Ele tem uma interface e automatiza muitas coisas que teríamos que fazer manualmente também! 
- **Links úteis:**  
  - [Site oficial](https://tilt.dev/)
  - [Documentação](https://docs.tilt.dev/)

---

### **yq**
- **O que é?**  
  Uma ferramenta que vamos instalar para manipular arquivos YAML em linha de comando, semelhante ao jq para JSON.
- **Para que serve?**  
  Edita, transforma e consulta arquivos YAML. São nos arquivos YAML que vamos escrever como vai ser a configuração das aplicações, serviços ou clusters.
- **Links úteis:**  
  - [GitHub do yq](https://github.com/mikefarah/yq)

---



