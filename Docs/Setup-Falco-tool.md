# Setting up Falco for cluster Monotoring and Logging

As an approach of prevention in security of any kuberentes cluster, we are going to use Falco on our cluster to observe the diffrent actions happening in our cluster,in order to detect any malicious activity. 

**Falco** is a behavioral activity monitor designed to detect anomalous activity in your applications. You can use Falco to monitor run-time security of your Kubernetes applications and internal components.

To get familiar with Falco, before running it on top of our hard-way cluster, we are going at first to run it on a cluster of our choice: Kind, Minikube, Kubeadmn. 

## 1) Minikube cluster:

Assuming you have Minikube installed, and  in case you don't, please follow these steps [here](https://kubernetes.io/docs/tasks/tools/install-minikube/).

Starting our cluster: `minikube start` and you should see your system pods running in few seconds. 

We are now moving to install Falco on our machine, because we need the driver loaded and running in our kernel, please follow these steps [here](https://falco.org/docs/installation/) 

We agree that we want to run Falco on each node of the cluster. So, we deploy it as a Daemon-Set using **Helm** chart as above:  

```
helm repo add falcosecurity https://falcosecurity.github.io/charts
helm repo update
```
values.yaml: 

```
image:  registry: docker.io
  repository: falcosecurity/falco
  tag: latest
ebpf:
  enabled: true
falco:
  fileOutput:
    enabled: false
    keepAlive: false
    filename: ./events.txt
```

 To install the chart with the release name falco run:

`helm upgrade --install  -f values.yaml  falco falcosecurity/falco`

Now that everything is on its place, you should be seeing a pod named falco-* in your cluster.
To see the logs redricting by Falco driver to your monitoring pod, you can run: 

`kubectl logs -f [falco pod] `. 
 
 ### Falco configuration:
 If you installed Falco the way above, you should have the rules configurations 'falco_rules.yaml' in /etc/falco. You find also 'falco_rules.local.yaml' for you to write your customized rules to monitor your cluster more efficienlty. Find more about configuration in this [section](https://falco.org/docs/configuration/
). 