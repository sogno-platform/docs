---
title: "Single Node Setup"
linkTitle: "Single Node Setup"
weight: 2
description: >
  Instructions on how to set up a single node kubernetes kluster for SOGNO.
---

## Prerequisites

The single node setup of SOGNO has been tested on the following operating systems:

* Ubuntu Server 20.04 LTS
* Ubuntu Desktop 20.04 LTS

## Installation

In order to run a single node SOGNO setup, we need to install kubernetes and the [helm](https://helm.sh/) package manager. [k3s]((https://k3s.io/)) is a powerful lightweight kubernetes installation that suites well for single node or edge deployments. Helm is a package manager for kubernetes. We aims at providing helm charts for simple deployment of the SOGNO platform and all our services to make the installation as easy as possible.

### K3s

First, we need to install a [k3s](https://k3s.io/) single node kubernetes cluster. Please refer to the official website for alternative installation methods. The simplest way is to use the official install script. Run the following command to download and execute the official installation script.

```
curl -sfL https://get.k3s.io | sh -
```

Afterwards, we can verify our installation was successful by running

```
sudo k3s kubectl get node
```

If the installation was successful, this should return a list of kubernetes nodes containing solely your host as a master node.

### Helm

[Helm](https://helm.sh/) is a package manager for kubernetes and provides detailed installation instructions on the website. Again, the fastest way is to use the provided install script:

```
curl -sfL https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 | bash
```

Now, we can varify the helm installation.

```
helm --kubeconfig /etc/rancher/k3s/k3s.yaml list
```
*Eventually, you might need to change the ownership of that file:*
```
sudo chown -R $USER /etc/rancher/k3s/
```

Finally, we can simplify the usage by setting the environment variable `KUBECONFIG` to our `k3s.yaml` file. By default (following our tutorial), it should be located in `/etc/rancher/k3s/`.

```
export KUBECONFIG=/etc/rancher/k3s/k3s.yaml
```
For a more convenient and persistent usage, you can also append it to your `.bashrc`

```
echo "export KUBECONFIG=/etc/rancher/k3s/k3s.yaml" >> ~/.bashrc
``` 

### Databus

One of the most central elements in the SOGNO architecture is the central databus. The current release uses MQTT over the [RabbitMQ](https://www.rabbitmq.com/) broker. We can install rabbitmq via helm:

```
helm repo add bitnami https://charts.bitnami.com/bitnami
helm install -n sogno-demo --create-namespace -f rabbitmq_values.yaml rabbitmq bitnami/rabbitmq 
```

The `rabbitmq_values.yaml` file contains SOGNO specific overwrites of the default rabbitMQ values. For our minimal single node setup, we can use the following values file:


```
extraPlugins: rabbitmq_mqtt

service:
  extraPorts:
    - name: mqtt
      port: 1883
      targetPort: 1883
  nodePort: LoadBalancer

auth:
  username: admin
  password: admin
```
