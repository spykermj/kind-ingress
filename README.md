# Ingress Controller on Kind

This was created based on [kind documentation](https://kind.sigs.k8s.io/docs/user/ingress/#ingress-nginx).

## Create Kind Cluster

```
kind create cluster --config=./kind-cluster.yaml
```

## Install NGINX Ingress Controller

```
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/kind/deploy.yaml
```

## Wait for the Ingress Controller to be Ready

```
kubectl wait --namespace ingress-nginx \
  --for=condition=ready pod \
  --selector=app.kubernetes.io/component=controller \
  --timeout=90s
```

## Use the Ingress

```
kubectl create ns testingress
kubectl -n testingress apply -f https://kind.sigs.k8s.io/examples/ingress/usage.yaml
```

