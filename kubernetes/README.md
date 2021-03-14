# Kubernetes

## Local

### Requirements

* install [kubectl](https://kubernetes.io/docs/tasks/tools/)
- install [minikube](https://minikube.sigs.k8s.io/docs/start/) (tested on `v1.18.1` version)
* start kubernetes with minikube
```shell
minikube start --addons=default-storageclass,ingress,ingress-dns,storage-provisioner \
               --memory='16gb' \
               --cpus=8
```
* install [helm 3](https://helm.sh/docs/intro/install/)

_for remove all: `minikube delete --all=true --purge=true`_

### Configure environment

* create namespace `kubectl apply -f namespace.yaml`

* postgres:
```shell
helm -n okfn-brasil \
     upgrade postgresql \
     -f postgresql-dev-values.yaml \
     bitnami/postgresql \
     --install \
     --version 10.3.13 \
     --atomic
```
* local access `kubectl port-forward --namespace okfn-brasil svc/postgresql 5432:5432`
