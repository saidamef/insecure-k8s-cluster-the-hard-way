FROM debian

MAINTAINER saidameft/kube-proxy:latest

RUN apt-get update -y && apt-get install -y iptables wget

RUN wget https://storage.googleapis.com/kubernetes-release/release/v1.17.3/kubernetes-server-linux-amd64.tar.gz && \
    tar xvf kubernetes-server-linux-amd64.tar.gz && \
    mv kubernetes/server/bin/kube-proxy  /usr/local/bin && \
    rm -r /kubernetes  && \
    rm -rf kubernetes-server-linux-amd64.tar.gz 

ENTRYPOINT [""]
