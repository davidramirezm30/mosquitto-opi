#
# Follow platform guideline specified in https://github.com/docker-library/official-images
# Reference:
#  - https://mosquitto.org/2013/01/mosquitto-debian-repository/
#

FROM arm32v7/debian:stretch
MAINTAINER David Ramirez <davidramirez.drm@gmail.com>
LABEL description="Eclipse Mosquitto MQTT Broker"
# Establecemos el frontend como no-interactivo
ENV DEBIAN_FRONTEND noninteractive
# Usamos un único RUN solo, para evitar generar muchas capas docker
RUN apt-get clean && apt-get update && apt-get install -y apt-utils && apt-get -y upgrade && \
    apt-get install -y apt-transport-https gnupg2
# Copiamos clave gpg y repo
COPY mosquitto-repo.gpg.key /
COPY mosquitto-stretch.list /etc/apt/sources.list.d/
COPY docker-entrypoint.sh /
# Instalamos mosquitto
RUN apt-key add mosquitto-repo.gpg.key && apt-get update && apt-get -y install mosquitto mosquitto-clients && \
    ## Tuneos varios mosquitto
    mkdir -p /mosquitto/config /mosquitto/data /mosquitto/log && \
    cp /etc/mosquitto/mosquitto.conf /mosquitto/config && \
    chown -R mosquitto:mosquitto /mosquitto /docker-entrypoint.sh && \
    chmod ug+x /docker-entrypoint.sh
VOLUME ["/mosquitto/config", "/mosquitto/data", "/mosquitto/log"]
ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["/usr/sbin/mosquitto", "-c", "/mosquitto/config/mosquitto.conf"]

