FROM alpine:latest
LABEL maintainer="Jurijs Kolomijecs <jurikolo@yandex.com>"
LABEL description="An image with the latest version on Consul."

ENV CONSUL_VERSION 0.8.5
ENV CONSUL_SHA256 35dc317c80862c306ea5b1d9bc93709483287f992fd0797d214d1cc1848e7b62
ENV CONSUL_UI_SHA256 4f7b90d8159480daeff6f3673f56fc75c00e4fd05de9c5c6d22a4af2fbc78368

RUN  apk add --update ca-certificates wget && \
     wget -O consul.zip https://releases.hashicorp.com/consul/${CONSUL_VERSION}/consul_${CONSUL_VERSION}_linux_amd64.zip && \
     echo "$CONSUL_SHA256 *consul.zip" | sha256sum -c - && \
     unzip consul.zip && \
     mv consul /bin/ && \
     rm -rf consul.zip && \
     cd /tmp && \
     wget -O ui.zip https://releases.hashicorp.com/consul/${CONSUL_VERSION}/consul_${CONSUL_VERSION}_web_ui.zip && \
     echo "$CONSUL_UI_SHA256 *ui.zip" | sha256sum -c - && \
     unzip ui.zip && \
     mkdir -p /ui && \
     mv * /ui && \
     rm -rf /tmp/* /var/cache/apk/*

EXPOSE 8300 8301 8301/udp 8302 8302/udp 8400 8500 8600 8600/udp

VOLUME [ "/data" ]

ENTRYPOINT [ "/bin/consul" ]
CMD [ "agent", "-data-dir", "/data", "-server", "-bootstrap-expect", "1", "-ui-dir", "/ui", "-client=0.0.0.0"]
