# Overview

Repository with scripts to configure and launch CloudBees Core on Google Container Enginer (GKE). This installation package supports 

# Getting Started

## Set Your GCP Config and Authenticate

```shell
gcloud config set project <GCP Project>
gcloud config set compute/zone <zone>
gcloud config set account <user>
gcloud auth login
```

## Create Your Cluster

See [Getting Started](https://github.com/GoogleCloudPlatform/marketplace-k8s-app-tools/blob/master/README.md#getting-started) to create your cluster. CloudBees Core requires a minimum 3 node cluster with each node having a minimum of 2 vCPU and k8s version 1.8.

Then:

```shell
gcloud container clusters get-credentials <cluster> 
```

## Installing CloudBees Core on Your Cluster

### Create your Namespace
```shell
kubectl create namespace <namespace>
export NAMESPACE=<namespace>
```

### One-time CRD Setup

```shell
make crd/install
```

### Install CloudBees Core on your Cluster

```shell
make app/install
```

### Monitor the Installation

```shell
make app/watch
```

### Setup Wizard
Get the CloudBees Core Operations Center URL:

```shell
kubectl get ing -n <namespace> | grep cjoc
```
Paste the domain name listed into your browser to go to the CloudBees Core Operations Center and start the setup process. The installation process requires an intial admin password. Execute this command to get it:

```shell
kubectl exec cjoc-0 -n <namespace> -- cat /var/jenkins_home/secrets/initialAdminPassword
```

Then follow the instructions in the setup wizard to complete the installation.

## Using CloudBees Core

### Getting Started Guide
To get started using CloudBees Core read our [Getting Started Guide](https://go.cloudbees.com/docs/cloudbees-core/cloud-admin-guide/getting-started/#).

### Additional Resources
[CloudBees Core Administration Guide](https://go.cloudbees.com/docs/cloudbees-core/cloud-admin-guide/)

[CloudBees Core Reference Architecture](https://go.cloudbees.com/docs/cloudbees-core/cloud-reference-architecture/)

### CloudBees Core Support
For CloudBees Core support, [visit the CloudBees support page](https://support.cloudbees.com/hc/en-us/requests).

### Delete the Installation (optional)

```shell
make app/uninstall
```

