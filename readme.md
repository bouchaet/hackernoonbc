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