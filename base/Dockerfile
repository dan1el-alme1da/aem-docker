# Usando Ubuntu como base
FROM ubuntu


# Define diretório de trabalho
WORKDIR /opt/aem


# Copia o SDK (JAR do AEM)
COPY instance.jar instance.jar


# Instala Java 11
RUN apt-get update && \
apt-get install -y curl && \
apt-get install -y software-properties-common && \
add-apt-repository ppa:openjdk-r/ppa && \
apt-get update && \
apt-get install -y openjdk-11-jdk


# Descompacta o Quickstart
RUN java -jar instance.jar -unpack


# Explicação:

# Usa Ubuntu como base.

# Copia o JAR do AEM.

# Instala Java 11 (requisito do AEM).

# Executa java -jar instance.jar -unpack para descompactar o Quickstart.