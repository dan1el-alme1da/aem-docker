# Usa a imagem base
FROM aem-base


# Expõe a porta 4503
EXPOSE 4503


# Inicia o AEM no modo Publish
CMD ["java", "-jar", "instance.jar", "-r", "publish", "-p", "4503"]

# Explicação:

# Define o contêiner como modo Publish (-r publish).

# Expõe a porta 4503 (padrão do Publish).