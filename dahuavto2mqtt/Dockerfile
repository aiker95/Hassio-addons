ARG BUILD_FROM=hassioaddons/base:7.0.3
# hadolint ignore=DL3006
FROM ${BUILD_FROM}

ENV LANG C.UTF-8

ARG DAHUA_BRANCH="master"

WORKDIR /app
COPY . /app

RUN apk add --no-cache --update argon2-libs php php-json && \
apk add --no-cache --virtual .build-dependencies git && \
git clone https://github.com/elad-bar/DahuaVTO2MQTT.git --branch ${DAHUA_BRANCH} --depth 1 /app_docker && \
mv /app_docker/DahuaEventHandler.php /app_docker/DahuaVTO.php && \
mv /app_docker/* /app/ && \
chmod +x /app/DahuaVTO.php && \
apk del .build-dependencies 

RUN ls /app

# Build arguments
ARG BUILD_DATE
ARG BUILD_REF
ARG BUILD_VERSION

# Labels
LABEL \
    io.hass.name="DahuaVTO2MQTT" \
    io.hass.description="Sends Dahua Intercom events to the MQTT Broker" \
    io.hass.arch="${BUILD_ARCH}" \
    io.hass.type="addon" \
    io.hass.version=${BUILD_VERSION} \
    maintainer="Elad Bar <elad.bar@hotmail.com>" \
    org.label-schema.description="Sends Dahua Intercom events to the MQTT Broker" \
    org.label-schema.build-date=${BUILD_DATE} \
    org.label-schema.name="DahuaVTO2MQTT" \
    org.label-schema.schema-version="1.0" \
    org.label-schema.url="https://community.home-assistant.io" \
    org.label-schema.usage="https://github.com/elad-bar/Hassio-addons/blob/master/README.md" \
    org.label-schema.vcs-ref=${BUILD_REF} \
    org.label-schema.vcs-url="https://github.com/elad-bar/Hassio-addons/" \
    org.label-schema.vendor="Hass.io Bar's add-on"

RUN chmod +x /app/run.sh

CMD /app/run.sh

