# 🧱 AEM com Docker — Ambiente Local Completo
 
> 🚀 Guia prático e didático para rodar **Adobe Experience Manager (AEM)** em containers Docker  
> 🐳 Com instâncias **Author** (porta 4502) e **Publish** (porta 4503)

---

## 🧩 Sumário

- [✨ Visão Geral](#-visão-geral)
- [🧰 Requisitos](#-requisitos)
- [📁 Estrutura do Projeto](#-estrutura-do-projeto)
- [🧱 Criando as Imagens Docker](#-criando-as-imagens-docker)
- [⚙️ Build das Imagens](#️-build-das-imagens)
- [🌐 Criar Rede Docker](#-criar-rede-docker)
- [🚀 Rodar Containers](#-rodar-containers)
- [🧠 Verificar Logs e Status](#-verificar-logs-e-status)
- [💡 Dicas e Boas Práticas](#-dicas-e-boas-práticas)

---

## ✨ Visão Geral

Este projeto demonstra como **executar o AEM localmente** dentro de containers Docker.  
O ambiente inclui:

- 🧩 **Imagem base** com AEM + Java 11  
- 🖥️ **Author instance** → Porta `4502`  
- 🌍 **Publish instance** → Porta `4503`  
- 🌐 Rede Docker `adobe` conectando ambos  

---

## 🧰 Requisitos

| Sistema | Requisito | Observações |
|----------|------------|-------------|
| 💻 **Windows/macOS** | Docker Desktop | **Execute o Docker Desktop antes de usar** |
| 🐧 **Linux** | Docker Engine | Instale via apt ou yum |
| ☕ **Java JDK 11** | Requisito do AEM | Necessário para o Quickstart |
| 📦 **AEM SDK** | Arquivo `.jar` | **OBRIGATÓRIO**: Baixe do portal da Adobe |
| 💾 **Recursos** | RAM e disco livres | O AEM pode consumir 4–8 GB RAM |

> ⚠️ **IMPORTANTE - FINS DIDÁTICOS**: 
> 
> Este projeto contém um `instance.jar` **PLACEHOLDER INVÁLIDO** para demonstração.
> 
> **Para funcionar, você DEVE:**
> 1. 📥 Baixar o **AEM SDK oficial** do Adobe Experience Manager
> 2. 🔄 Substituir o arquivo `instance.jar` pelo arquivo real
> 3. 🚫 Nunca publique o arquivo real em repositórios públicos!
> 
> **Sem o AEM SDK real, os containers falharão com "Invalid or corrupt jarfile"**

---

## 📁 Estrutura do Projeto

```
aem-docker/
├── base/
│   └── Dockerfile
├── author/
│   └── Dockerfile
├── publish/
│   └── Dockerfile
└── instance.jar    # ⚠️ PLACEHOLDER - Substitua pelo AEM SDK real
```

---

## 🧱 Criando as Imagens Docker

### 1️⃣ Imagem Base (`base/Dockerfile`)

```dockerfile
FROM ubuntu

WORKDIR /opt/aem

# Instala Java 11
RUN apt-get update && \
    apt-get install -y openjdk-11-jdk && \
    rm -rf /var/lib/apt/lists/*

# Copia o SDK (JAR do AEM) - substitua pelo arquivo real
COPY instance.jar instance.jar
```

### 2️⃣ Imagem Author (`author/Dockerfile`)

```dockerfile
FROM aem-base
EXPOSE 4502
CMD ["java", "-jar", "instance.jar", "-r", "author", "-p", "4502"]
```

### 3️⃣ Imagem Publish (`publish/Dockerfile`)

```dockerfile
FROM aem-base
EXPOSE 4503
CMD ["java", "-jar", "instance.jar", "-r", "publish", "-p", "4503"]
```

---

## ⚙️ Build das Imagens

**Execute os comandos UM POR VEZ na ordem:**

```bash
# 1. Primeiro a imagem base
docker build -f base/Dockerfile -t aem-base .

# 2. Depois o author
docker build -f author/Dockerfile -t aem-author .

# 3. Por último o publish
docker build -f publish/Dockerfile -t aem-publish .
```
![alt text](<Captura de tela 2025-10-20 163254.png>)

---
![alt text](<Captura de tela 2025-10-20 163419.png>)

## 🌐 Criar Rede Docker

```bash
docker network create adobe
```

---

## 🚀 Rodar Containers

> ⚠️ **ATENÇÃO**: Só funcionará com o AEM SDK real!

```bash
# Author
docker run -d --name author -p 4502:4502 --network adobe aem-author

# Publish
docker run -d --name publish -p 4503:4503 --network adobe aem-publish
```

---

## 🧠 Verificar Logs e Status

```bash
# Ver containers
docker ps

# Ver logs
docker logs -f author
```

**Aguarde a mensagem:** `Quickstart started`

👉 **Acesse:**
- Author → [http://localhost:4502](http://localhost:4502)
- Publish → [http://localhost:4503](http://localhost:4503)

---

## 💡 Dicas e Boas Práticas

**Limpar containers:**
```bash
docker stop author publish && docker rm author publish
```

**Adicionar ao `.gitignore`:**
```
instance.jar
```

**Testar estrutura sem AEM:**
```bash
docker build -f test-dockerfile -t aem-test .
docker run --rm aem-test
```

---

### 👨💻 Projeto Didático

Baseado no artigo: [Lucas Ribeiro – *AEM with Docker*](https://medium.com/@lucasnunesr/aem-with-docker-07b2404feeb2)

Adaptado para fins educacionais por Daniel Almeida ✨