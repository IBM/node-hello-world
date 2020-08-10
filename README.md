# Minimal Node.js Hello World example

This repo contains a minimal hello world application written in Node. This repo will document the many ways you can deploy this application.

## Run locally

```bash
npm install
npm start
```

## Run in a container

```bash
docker build -f Dockerfile -t hello-world-node:latest .
docker run -it -p 8080:8080 --name hello-world-node hello-world-node:latest
```

### Run on Cloud Foudry

```bash
cf push
```

## Run on IBM Kubernetes Service

Ensure the container image URL is updated in [deployment.yaml](config/deployment.yaml).

```bash
# ibmcloud login  -r us-south -g default
# ibmcloud cr region-set us-south
# ibmcloud cr login

# build and push to ICR
# update the container registry to match your own namespace
docker build -t us.icr.io/samples/hello-world-node:v1 .
docker push us.icr.io/samples/hello-world-node:v1

# deploy to IKS
# update the cluster id field to match your IKS instance
ibmcloud ks cluster config --cluster <cluster-id>
kubectl config current-context
kubectl apply -f config/
kubectl rollout status deployment/hello-world-node
kubectl get services -o wide
```

### Run on OpenShift

```bash
oc new-app
```
