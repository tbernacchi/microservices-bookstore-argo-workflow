FROM openliberty/open-liberty:latest

ENV SERVERDIRNAME reviews

# Copia o servidor de configuração para o container
COPY ./servers/LibertyProjectServer /opt/ibm/wlp/usr/servers/defaultServer/

# Instala as features automaticamente a partir do server.xml
RUN /opt/ol/wlp/bin/featureUtility installServerFeatures --acceptLicense /opt/ibm/wlp/usr/servers/defaultServer/server.xml

# Define variáveis de ambiente para o serviço
ARG service_version
ARG enable_ratings
ARG star_color
ENV SERVICE_VERSION ${service_version:-v1}
ENV ENABLE_RATINGS ${enable_ratings:-false}
ENV STAR_COLOR ${star_color:-black}

# Comando para iniciar o servidor
CMD ["/opt/ibm/wlp/bin/server", "run", "defaultServer"]

