## Getting started locally with docker

### Pre-requisites

#### With boot2docker
- Install [boot2docker](http://boot2docker.io/) 
```
boot2docker up
export DOCKER_HOST_IP=$(boot2docker ip)
export KUBERNETES_MASTER=$DOCKER_HOST_IP:8080
export BOOT2DOCKER=y
```

#### With local docker daemon
```
export DOCKER_HOST_IP=127.0.0.1
export KUBERNETES_MASTER=$DOCKER_HOST_IP:8080
```

### Build the kubernetes docker images

```
BUILD_RUN_IMAGES=y ./build/make-run-image.sh 
```

### Bootstrap the cluster

```
docker run -p 10250:10250 -v /var/run/docker.sock:/var/run/docker.sock kubernetes-bootstrap
```

### Manage your pods
```
kubecfg list /pods
kubecfg -p 8181:80 run nginx 1 kube-nginx
kubecfg list /pods
curl $DOCKER_HOST_IP:8181
```
