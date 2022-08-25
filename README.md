# Monokle Demo - CRDs with Istio

Interactively discover Monokle with these examples.

## Prerequisite

Create a cluster, for instance with minikube:

```bash
minikube start
```

Let's already open a tunnel since the deployment will use a LoadBalancer service:

```bash
minikube tunnel
```

## How to deploy this demo

1. Deploy the namespace

```bash
kubectl apply -f namespaces
```

2. Deploy Istio

Note: These manifests are generated with `istioctl`. It is recommended to commit these manifests in git so you can conveniently view changes before you apply them to the cluster and have an audit trail.

```bash
kubectl apply -f platform
```

The command that was used to generate the issues is (see [this issue](https://github.com/istio/istio/issues/36762#issuecomment-1205513455) for why these value are overriden):

````
istioctl manifest generate \
    --set values.global.hub=gcr.io/istio-testing \
    --set values.global.tag=1.16-alpha.db637b3e4d3c09da0f8fc8f3222231e1834668ed > platform/istio.yaml
```

1. Deploy the sample application

```bash
kubectl apply -f apps
```

4. Expose your application with Istio

```bash
kubectl apply -f networking
```

5 Visit the application by opening [localhost/productpage](http://localhost/productpage).
````
