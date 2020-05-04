
# Running Istio on Minikube

## Minikube Prerequisite

4 CPUs and 16Gb RAM

To configure Minikube
```
# set cpu and ram
minikube config set memory 16384
minikube config set cpus 4

# for macos, set driver as virtualbox
minikube config set vm-driver virtualbox

# delete previous vm image
minikube delete

# start with new settings
minikube start
```

[More details](https://istio.io/docs/setup/platform-setup/minikube/)

## Install Istio

Following these [instructions](https://istio.io/docs/setup/getting-started/), I was able to get Istio and sample application running on my minikube.
