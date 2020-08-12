# Minimal Node.js Hello World example

This repo contains a minimal hello world application written in Node. This repo will document the many ways you can deploy this application.

## Run locally

```bash
npm install
npm start
```

## Run in a container

```bash
docker build -t node-hello-world:latest .
docker run -it -p 8080:8080 --name node-hello-world node-hello-world:latest
```

## Run on Cloud Foudry

Details about the Cloud Foundry deployment can be found in [manifest.yml](manifest.yml).

```bash
# target a cloud foundry region
ibmcloud target --cf

# push the app
ibmcloud cf push
```

## Run on IBM Kubernetes Service

Ensure the container image URL is updated in [deployment.yaml](config/deployment.yaml).

```bash
# ibmcloud login  -r us-south -g default
# ibmcloud cr region-set us-south
# ibmcloud cr login

# build and push to ICR
# update the container registry to match your own namespace
docker build -t us.icr.io/samples/node-hello-world:v1 .
docker push us.icr.io/samples/node-hello-world:v1

# deploy to IKS
# update the cluster id field to match your IKS instance
ibmcloud ks cluster config --cluster <cluster-id>
kubectl config current-context
kubectl apply -f config/
kubectl rollout status deployment/node-hello-world
kubectl get services -o wide
```

## Run on OpenShift

```bash
oc login
oc new-project samples
oc new-app nodejs~https://github.com/ibm/node-hello-world.git
oc expose svc/node-hello-world
oc get routes
```
