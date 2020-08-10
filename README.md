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
docker run -it -p 8080:8080 --name hello_node hello-world-node:latest
```

### Run on Cloud Foudry

```bash
cf push
```

## Run on Kubernetes

```bash
kubectl
```

### Run on OpenShift

```bash
oc new-app
```
