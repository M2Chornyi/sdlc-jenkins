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
### 
