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
postgresql.okfn-brasil.svc.cluster.local

* memcached:
```shell
helm -n okfn-brasil \
     upgrade memcached \
     -f memcached-dev-values.yaml \
     bitnami/memcached \
     --install \
     --version 5.7.0 \
     --atomic
```
* local access `kubectl port-forward --namespace okfn-brasil svc/postgresql 11211:11211`
memcached.okfn-brasil.svc.cluster.local

* rabbitmq:
```shell
helm -n okfn-brasil \
     upgrade rabbitmq \
     -f rabbitmq-dev-values.yaml \
     bitnami/rabbitmq \
     --install \
     --version 8.11.3 \
     --atomic
```
* local access `kubectl port-forward --namespace okfn-brasil svc/rabbitmq 5672:5672`
rabbitmq.okfn-brasil.svc.cluster.local

    echo "URL : amqp://127.0.0.1:5672/"
    kubectl port-forward --namespace okfn-brasil svc/rabbitmq 5672:5672

To Access the RabbitMQ Management interface:

    echo "URL : http://127.0.0.1:15672/"
    kubectl port-forward --namespace okfn-brasil svc/rabbitmq 15672:15672

