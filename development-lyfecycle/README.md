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
  TH3_VERSION=0.0.1 ; \
  STACK=blue ; \
  helm upgrade -i $STACK th3-server --set image.tag=$TH3_VERSION --set stack=$STACK ;
```
### Test: 
Please run in duplicate terminal window:
```shell
 kubectl run testbox --image=nginx --restart=Never --rm -it -- bash
  # while sleep 2; do curl application/version ; done
```
### Create `appication` service in kubernetes to expose desired application:
```shell
  kubectl create service loadbalancer application --tcp=80:8080 ; \
  kubectl patch service application --type='json' -p='[{"op": "replace", "path": "/spec/selector", "value":{ "stack": "'$STACK'" } }]'
  # kubectl create ingress blizzard --rule=blue.local/blue/*=blue-th3-server:8080 --rule=green.local/green/*=green-th3-server:8080  --rule=bizzard.local/*=green-th3-server:8080 
```
### Switch `service/application` to LIVE stack:
```shell
LIVESTACK=green ; \
kubectl patch service application --type='json' -p='[{"op": "replace", "path": "/spec/selector", "value":{ "stack": "'$LIVESTACK'" } }]'
```