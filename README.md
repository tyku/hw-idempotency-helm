# Homework idempotency

## Install order service

namespace default
```bash
helm install order ./app -f ./order-service/values.yaml
```

## Installation nginx ingress

Add repo
```bash
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm repo update
```
Install nginx-ingress
```bash
helm install --version "3.35.0" -n nginx-ingress -f ./nginx-ingress/nginx.yaml \
ingress-nginx ingress-nginx/ingress-nginx
```

Apply routes
```bash
kubectl apply -f ./nginx-ingress/routes.yaml

minikube service -n nginx-ingress ingress-nginx-controller
```

If you are using minikube, turn on ingress addon with command
```bash
minikube addons  enable ingress
```


## Uninstall

```bash
helm un order
```


## Tests
Install newman if you wish:
```
brew install newman
```
and run prepared test
```
newman run ./hw_stream_processing.postman_collection.json
```
or import this file to postman, and start manually

Link to course: https://otus.ru/lessons/microservice-architecture