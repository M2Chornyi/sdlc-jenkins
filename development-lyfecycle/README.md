## Prerequisites:
- Installed `minikube` or `kubernetes`
- Installed `helm`
---
## Tasks
### Create application images:
- Update project files and create different version of application, simple change is to made version change in file `th3-server.py`
- Create/build docker image and install it to each node:
```shell
  version=0.0.1
  # for minikube run command before build:  eval $(minikube -p minikube docker-env)
  docker build -t th3-python:0.0.1 .
```
**NOTE:** in this exercise we assume that the current image is installed on each running node.
### Create helm chart for application rollout:
```shell
  TH3_VERSION=0.0.2 ; \
  STACK=green ; \
  helm upgrade -i $STACK th3-server --set image.tag=$TH3_VERSION --set stack=$STACK ;
```
### Create `appication` service in kubernetes to expose desired application:
```shell
  kubectl create service loadbalancer application --tcp=80:8080 ; \
  kubectl patch service application --type='json' -p='[{"op": "replace", "path": "/spec/selector", "value":{ "stack": "'$STACK'" } }]'
```
