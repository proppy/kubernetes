## Getting started on boot2docker

### Requirements 

- Install [boot2docker](http://boot2docker.io/).

### Building the kubernetes docker images

```
BOOT2DOCKER=y BUILD_RUN_IMAGES=y ./build/make-run-image.sh 
```

### Bootstrap the cluster

```
docker run -p 10250:10250 -v /var/run/docker.sock:/var/run/docker.sock kubernetes-bootstrap
```

### Manage your pods
```
export KUBERNETES_MASTER=$(boot2docker ip):8080
kubecfg list /pods
kubecfg -p 8181:80 run nginx 1 kube-nginx
kubecfg list /pods
curl $(boot2docker ip):8181
```
