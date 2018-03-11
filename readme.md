# Hackernoon Blockchain
Simply following this [post](https://hackernoon.com/learn-blockchains-by-building-one-117428612f46).

# Prerequisite
Python 3.6 or higher

# Usage
```
> python --version
> virtualenv env && env/scripts/activate
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
> In fact, the image will use resin base image that is not base on stretch 
specifically on the _a_ debian distro. 
More information on [dockerhub.io/resin](https://hub.docker.com/r/resin/raspberrypi3-python/).


# Kubernetes (rasp-pi cluster)
## Creation
```
> kubectl create -f k8s-deployment.yaml
> kubectl rollout status deployment hackernoonbc-deployment 
> kubectl create -f k8s-service.yaml
```
> This image can also be runned locally on a amd64 architecture by activating `qemu-user-static` on linux. Information is available on [multiarch/qemu-user-static](https://github.com/multiarch/qemu-user-static/blob/master/README.md). Basically, the command is:   
`> docker run --rm --privileged multiarch/qemu-user-static:register --reset`
## Delete
```
> kubectl delete deployment hackernoonbc-deployment 

```

## Get an image hash tag
Here's how to pull the latest image from a kubectl deployment. The hash tag will force
a pull of the image if the it has changed. Using a tag will (say latest) will pull the image
from the cache if available.
```
> docker inspect --format='{{.RepoDigests}}' bouchaet/hackernoonbc:stretch
```
