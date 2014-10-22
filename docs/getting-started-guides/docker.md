## Getting started locally with docker

### Pre-requisites

#### With boot2docker
- Install [boot2docker](http://boot2docker.io/) 
```
boot2docker up
$(boot2docker shellinit)
export DOCKER_HOST=$(boot2docker ip 2>/dev/null)
export KUBERNETES_MASTER=$DOCKER_HOST_IP:8080
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
docker run -v /var/run/docker.sock:/var/run/docker.sock kubernetes-bootstrap
```

### Get kubernetes release
curl -L https://github.com/GoogleCloudPlatform/kubernetes/releases/download/v0.4.1/kubernetes.tar.gz | tar xvzf -
export PATH=/path/to/kubernetes/platforms/os/arch:$PATH

### Manage your pods
```
kubecfg list /pods
kubecfg -p 8181:80 run nginx 1 kube-nginx
kubecfg list /pods
curl $DOCKER_HOST_IP:8181
```
