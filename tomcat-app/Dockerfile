FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive
ENV JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
ENV PATH=$PATH:/opt/tomcat/bin

# Instala dependências e OpenJDK 8
RUN apt-get update && \
    apt-get install -y openjdk-8-jdk curl wget unzip && \
    rm -rf /var/lib/apt/lists/*

# Instala Apache Tomcat 8.5
RUN mkdir -p /opt/tomcat && \
    curl -fSL https://archive.apache.org/dist/tomcat/tomcat-8/v8.5.96/bin/apache-tomcat-8.5.96.tar.gz | \
    tar -xzC /opt/tomcat --strip-components=1

# Copia o arquivo tomcat-users.xml (você deve ter este arquivo no mesmo diretório do Dockerfile)
COPY tomcat-users.xml /opt/tomcat/conf/

# Remove restrição de IP do Manager App (libera acesso externo)
RUN sed -i 's|allow=".*"|allow=".*"|' /opt/tomcat/webapps/manager/META-INF/context.xml

# Expõe a porta do Tomcat
EXPOSE 8080

# Inicia o Tomcat
CMD ["/opt/tomcat/bin/catalina.sh", "run"]
