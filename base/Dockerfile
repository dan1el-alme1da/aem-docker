# Usando Ubuntu como base
FROM ubuntu


# Define diretório de trabalho
WORKDIR /opt/aem


# Instala Java 11
RUN apt-get update && \
    apt-get install -y openjdk-11-jdk && \
    rm -rf /var/lib/apt/lists/*

# Copia o SDK (JAR do AEM) - substitua pelo arquivo real
COPY instance.jar instance.jar


# Explicação:

# Usa Ubuntu como base.

# Copia o JAR do AEM.

# Instala Java 11 (requisito do AEM).

# Executa java -jar instance.jar -unpack para descompactar o Quickstart.