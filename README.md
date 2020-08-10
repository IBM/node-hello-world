# Minimal Node.js Hello World example

This repo contains a minimal hello world application written in Node. This repo will document the many ways you can deploy this application.

## Run locally

```bash
$ npm install
$ npm start
```

## Run in a container

```bash
$ docker build -f Dockerfile -t hello-python:latest .
$ docker run -it -p 5001:5001 --name hello_python hello-python:latest
```

### Run on Cloud Foudry

```bash
$ cf push
```

## Run on Kubernetes

```bash
$ kubectl
```

### Run on OpenShift

```bash
$ oc new-app
```
