FROM ubuntu:16.04
RUN apt-get update && \
apt-get install unzip wget curl vim -y

WORKDIR /home/ubuntu/ 

ENV VAULT_ADDR https://server.dc1.consul:8200

RUN wget https://releases.hashicorp.com/vault/1.1.3/vault_1.1.3_linux_amd64.zip
RUN unzip vault_1.1.3_linux_amd64.zip
RUN mv vault /usr/bin

RUN mkdir /etc/vault
COPY ui.json /etc/consul.d/ui.json
COPY certs .


RUN cat consul-agent-ca.pem >> /etc/ssl/certs/ca-certificates.crt
RUN echo "127.0.0.1 server.dc1.consul" >> /etc/hosts

COPY config.hcl /etc/vault/config.hcl

CMD /usr/bin/vault server -config=/etc/vault/config.hcl