# Hackernoon Blockchain
[![Build Status](https://travis-ci.org/bouchaet/hackernoonbc.svg?branch=master)](https://travis-ci.org/bouchaet/hackernoonbc)  
Simply following this [post](https://hackernoon.com/learn-blockchains-by-building-one-117428612f46).

# Prerequisite
Python 3.6 or higher

# Usage
```
> python --version
> virtualenv env && . env/scripts/activate
> pip3 install -r requirements.txt
> python blockchain.py
```

# Docker
## Run locally
```
> docker build -t bouchaet/hackernoonbc:latest .
> docker run -rm -d -p 5000:5000 --name hackernoonbc hackernoonbc
```
## Push on docker hub
```
> docker push bouchaet/hackernoonbc:latest
```
## Build for stretch (rasp-pi cluster)
```
> docker build -t bouchaet/hackernoonbc:stretch . -f Dockerfile.stretch
> docker push bouchaet/hackernoonbc:stretch
```
> In fact, the image will use **resin.io** base image that is not build from stretch 
specifically but on _a_ debian distro. 
More information on [dockerhub.io/resin](https://hub.docker.com/r/resin/raspberrypi3-python/).
> This image can also be runned locally on a amd64 architecture by activating `qemu-user-static` on linux. Information is available on [multiarch/qemu-user-static](https://github.com/multiarch/qemu-user-static/blob/master/README.md). Basically, the command is:   
`> docker run --rm --privileged multiarch/qemu-user-static:register --reset`

# Kubernetes (rasp-pi cluster)
## Creation
```
> kubectl create -f k8s-deployment.yaml
> kubectl rollout status deployment hackernoonbc-deployment 
> kubectl create -f k8s-service.yaml
```
## Delete
```
> kubectl delete deployment hackernoonbc-deployment 
```

## Get an image hash tag. 
Use the hash tag to pull the latest image from a kubectl deployment. However, other techniques may be available. 
The hash tag will force a pull if image was changed. Using a tag, like _:latest_, will pull the image
from the cache if present locally. Thus, remote updates will not be pulled. [see discussion](https://github.com/kubernetes/kubernetes/issues/33664)
```
> docker inspect --format='{{.RepoDigests}}' bouchaet/hackernoonbc:stretch
```
