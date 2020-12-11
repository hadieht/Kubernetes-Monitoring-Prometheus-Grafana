# Monitoring Kubernetes  clusters  using Prometheus and Grafana 



## Features
* Prometheus Operator with support for Prometheus v2.X.X
* highly available Prometheus and Alertmaneger
* auto-discovery for services and pods
* automatic RBAC configuration
* preconfigured alerts
* preconfigured Grafana dashboards
* easy to setup; usually less than a minute to deploy a complete monitoring solution for Kubernetes
* support for Kubernetes  v1.7.x and up running in  **AWS**, **GCP** and **Azure**


## Prerequisites

* Kubernetes cluster and `kubectl` configured
* Security Groups configured to allow the following ports:
     * 9100/TCP  -                node-exporter
     * 10250/TCP -                kubernetes nodes metrics,
     * 10251/TCP -                kube-scheduler
     * 10252/TCP -                kube-controller-manager
     * 10054/TCP and 10055/TCP -  kube-dns

#### Optional
* SMTP Account for email alerts


#### Running Kubernetes 1.12 and up?
If you are running Kubernetes 1.12 or higher you will also need to run [cAdvisor](https://github.com/google/cadvisor/tree/master/deploy/kubernetes) on your cluster (bound to host port 4194) in order to access resource usage and performance characteristics of running containers. 

## Pre-Deployment

Create monitoring namespace in Kubernetes

```shell
kubectl create namespace monitoring
```

## Deploy

Use kubectl to apply files in the folders

Now you can access the dashboards locally using `kubectl port-forward`command, or expose the services using a ingress or a LoadBalancer. 


## Updating configurations

  * **update alert rules:** add or change the rules in `prometheus/prometheus-configmap.yaml` .Then apply the changes using `kubectl apply -f prometheus/prometheus-configmap.yaml -n monitoring`

## Features

- Total and used cluster resources: CPU, memory, filesystem.  
  And total cluster network I/O pressure.  
  ![Total and used cluster resources](https://raw.githubusercontent.com/hadieht/kubernetes-monitoring-prometheus-grafana/main/screenshots/total.png)
- [Kubernetes pods](http://kubernetes.io/docs/user-guide/pods) usage:
  CPU, memory, network I/O.  
  ![Pods usage](https://raw.githubusercontent.com/hadieht/kubernetes-monitoring-prometheus-grafana/main/screenshots/pods.png)
- Containers usage: CPU, memory, network I/O.  
  [Docker](https://www.docker.com) containers
  which runs on cluster nodes but outside Kubernetes are also monitored.  
  ![Containers usage](https://raw.githubusercontent.com/hadieht/kubernetes-monitoring-prometheus-grafana/main/screenshots/containers.png)
- [systemd](https://freedesktop.org/wiki/Software/systemd) system services
  usage: CPU, memory.  
  ![systemd usage](https://raw.githubusercontent.com/hadieht/kubernetes-monitoring-prometheus-grafana/main/screenshots/systemd.png)
- Showing all above metrics both for all cluster and each node separately.  
  ![Filtering metrics by nodes](https://raw.githubusercontent.com/hadieht/kubernetes-monitoring-prometheus-grafana/main/screenshots/by_nodes.png)

