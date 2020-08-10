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
# target a cloud foundry region
ibmcloud target --cf

# push the app
ibmcloud cf push hello-world-node
```

> **NOTE**: We should have a `manifest.yml` defined for Cloud Foundry but we can bypass that as it auto-detects Node is required because of the `package.json` file in the top level.

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
oc login
oc new-project samples
oc new-app nodejs~https://github.com/ibm/node-hello-world-minimal.git
oc expose svc/node-hello-world-minimal
oc get routes
```
