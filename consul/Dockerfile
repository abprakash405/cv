FROM ubuntu:16.04
RUN apt-get update && \
apt-get install unzip wget curl vim -y

WORKDIR /home/ubuntu/ 

ENV CONSUL_HTTP_ADDR https://server.dc1.consul:8501

RUN wget https://releases.hashicorp.com/consul/1.5.2/consul_1.5.2_linux_amd64.zip
RUN unzip consul_1.5.2_linux_amd64.zip
RUN mv consul /usr/bin

RUN mkdir /etc/consul.d/ 
COPY ui.json /etc/consul.d/ui.json
COPY certs .
#RUN consul tls ca create
#RUN consul tls cert create -server


RUN cat consul-agent-ca.pem >> /etc/ssl/certs/ca-certificates.crt 
RUN echo 127.0.0.1 server.dc1.consul >> /etc/hosts

CMD /usr/bin/consul agent -server -ui -data-dir=/tmp/consul -bootstrap-expect=1 -node=vault -bind=0.0.0.0 -config-dir=/etc/consul.d/
