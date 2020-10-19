# insecure-k8s-cluster

## Manifest folder:

First, make sure to disable swap memory: `swapff -a` 

Then, make sure to run kubelet as systemd service, by placing kubelet/kubelet.service under /etc/systemd/system/ 

You find static pods configurations in the manifests folder in which you can invoke with with this command: 
`./kubelet --pod-manifest-path=./manifests --register-node=true --kubeconfig=kubelet.conf`
or as a Systemd service by : `systemctl enable kubelet.service ` , `systemctl start kubelet.service`

To check the status of your systemd service, run `systemctl status kubelet.service`

NB: make sure when you clone the repo, to work inside the porject, else you have to change the path mentionned into where you work in terminal. 

`docker ps ` you should see the 4 running containers of the componants : kube-api-server, kube-etcd, kube-scheduler, kube-controller-manager. 
To be able to enter to a components for updating: `docker exec -it <container> --rm /bin/sh `

Before you use kubectl client to test if you have your containers running as static pods, you should configure the kubectl: 

`kubectl config set-cluster kube --server=http://localhost:8080`

`kubectl config set-credentials kube`

`kubectl config set-context kube --cluster=kube --user=kube`

`kubectl config use-context kube` 
To check your configuration of kubectl: `kubectl config view`

Now, you can check your running static pods : `kubectl get pods -n kube-system`

## Kube-proxy: 
Now, in order to render your services accessible in our outside your hard-way cluster, you have to run a proxy component as Kube Daemon-set: `kubectl apply -f ./kube-proxy/kube-proxy.yaml`


## Docker images:

https://hub.docker.com/repository/docker/saidameft/kube-controller-manager

https://hub.docker.com/repository/docker/saidameft/kube-scheduler

https://hub.docker.com/repository/docker/saidameft/kube-apiserver

https://hub.docker.com/repository/docker/saidameft/etcd

https://hub.docker.com/repository/docker/saidameft/kube-proxy

kubelet version: Kubernetes v1.17.3
