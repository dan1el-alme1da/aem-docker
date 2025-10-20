# 📦 Como Obter o AEM SDK

## ⚠️ IMPORTANTE - FINS DIDÁTICOS

Este projeto contém um arquivo `instance.jar` **PLACEHOLDER** que não funciona.

## 🔧 Para Funcionar:

### 1. Obter o AEM SDK
- Acesse o [Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment/aem-runtime.html)
- Baixe o **AEM SDK Quickstart JAR**
- Renomeie para `instance.jar`

### 2. Substituir o Arquivo
```bash
# Remova o placeholder
rm instance.jar

# Copie o arquivo real do AEM SDK
cp /caminho/para/aem-sdk-quickstart.jar instance.jar
```

### 3. Executar o Projeto
```bash
docker build -f base/Dockerfile -t aem-base .
docker build -f author/Dockerfile -t aem-author .
docker build -f publish/Dockerfile -t aem-publish .
```

## 🚫 Nunca Versione o Arquivo Real
O arquivo `instance.jar` real está no `.gitignore` por motivos de licenciamento.

## 📚 Recursos
- [AEM Documentation](https://experienceleague.adobe.com/docs/experience-manager-65.html)
- [Docker Documentation](https://docs.docker.com/)