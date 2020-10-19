FROM docker.io/alpine:3.7
MAINTAINER saidameft/kube-apiserver:latest

RUN wget https://storage.googleapis.com/kubernetes-release/release/v1.17.3/kubernetes-server-linux-amd64.tar.gz && \
    tar xvf kubernetes-server-linux-amd64.tar.gz && \
    mv kubernetes/server/bin/kube-apiserver /usr/local/bin && \
    rm -r /kubernetes  && \
    rm -rf kubernetes-server-linux-amd64.tar.gz 

ENTRYPOINT ["kube-apiserver"]
