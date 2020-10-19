FROM docker.io/alpine:3.7
MAINTAINER saida/etcd:latest
RUN wget https://github.com/etcd-io/etcd/releases/download/v3.3.13/etcd-v3.3.13-linux-amd64.tar.gz && \
    tar xvf etcd-v3.3.13-linux-amd64.tar.gz && \
    mv etcd-v3.3.13-linux-amd64/etcd /usr/local/bin  && \
    mv etcd-v3.3.13-linux-amd64/etcdctl /usr/local/bin && \
    etcd --version && \
    rm -rf etcd.tar.gz etcd-* && \
    chmod +x /usr/local/bin 

 
	


#HEALTHCHECK --interval=5s --retries=3 --timeout=10s CMD ETCDCTL_API=3 /bin/etcdctl --endpoints=http://127.0.0.1:2379 get ping | grep -q pong

ENTRYPOINT ["etcd"]  


