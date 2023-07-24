# docker build -t weblogic-server:12c .
# docker run -d -p 7001:7001 --name wls-container weblogic-server:12c

# Use uma imagem base do Oracle Linux
FROM oraclelinux:8-slim

# Copie o arquivo de instalação do WebLogic Server para o contêiner
COPY fmw_12.2.1.4.0_wls_Disk1_1of1.zip /tmp/

# Instale o JDK (JRE também pode ser suficiente)
RUN yum -y install java-1.8.0-openjdk-devel

# Descompacte o arquivo de instalação do WebLogic Server e instale
RUN unzip /tmp/fmw_12.2.1.4.0_wls_Disk1_1of1.zip -d /tmp/install && \
    java -jar /tmp/install/fmw_12.2.1.4.0_wls.jar -silent -responseFile /tmp/install/response_file.txt && \
    rm -rf /tmp/install

# Defina as variáveis de ambiente necessárias para o WebLogic Server
ENV MW_HOME=/u01/oracle/wls12214
ENV WLS_HOME=$MW_HOME/wlserver
ENV PATH=$PATH:$WLS_HOME/server/bin:$MW_HOME/oracle_common/common/bin

# Exponha a porta do WebLogic Server
EXPOSE 7001

# Comando de inicialização
CMD ["/u01/oracle/wls12214/user_projects/domains/base_domain/startWebLogic.sh"]
