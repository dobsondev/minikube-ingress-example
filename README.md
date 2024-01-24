# Minikube Ingress Example

Pre-requisites:

1. Install [Docker](https://www.docker.com/)
2. Install [kubectl](https://kubernetes.io/docs/tasks/tools/#kubectl)
2. Install [Minikube](https://minikube.sigs.k8s.io/docs/start/)

## Commands

This generally follows this tutorial but a few steps are different:

- https://kubernetes.io/docs/tasks/access-application-cluster/ingress-minikube/


Start Minikube, enable the NGINX Ingress Controller and verify it is running:
```
minikube start
minikube addons enable ingress
kubectl get pods -n ingress-nginx
```

Next, we want to deploy a "Hello, World" app and create it's service. We then just quickly want to verify the pod and the service are running as expected:

```
kubectl apply -f deployment.yaml
kubectl get pods
kubectl get service web
```

Create the ingress object and verify the IP address is set:

```
kubectl apply -f ingress.yaml
kubectl get ingress
```

Append `127.0.0.1 hello-world.info` to your `/etc/hosts` file on MacOS (NOTE: Do **NOT** use the Minikube IP).

Run the following command (and keep the terminal window open) to open up a Minikube tunnel to the ingress. This command may prompt you for your sudo password:

```
minikube tunnel
```

Go to [http://hello-world.info/](http://hello-world.info/) and you should see the sample application running.