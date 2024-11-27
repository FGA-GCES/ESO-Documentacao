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

---
### **HOA**

---

### **Ingress**

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



