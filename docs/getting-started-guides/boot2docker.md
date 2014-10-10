## Getting started on boot2docker

### Requirements 

- Install [boot2docker](http://boot2docker.io/).

### Building the kubernetes docker images

```
BOOT2DOCKER=y BUILD_RUN_IMAGES=y ./build/make-run-image.sh 
```

### Bootstrap the cluster

```
docker run -p 10250:10250 -v /var/run/docker.sock:/var/run/docker.sock kubernetes /kubernetes/kubelet -v=5 -address=0.0.0.0 -hostname_override=10.0.2.15 -etcd_servers=http://10.0.2.15:4001 -config /pods/cluster-pod.yaml
```

### Manage your pods
```
export KUBERNETES_MASTER=$(boot2docker ip):8080
kubecfg list /pods
kubecfg -p 8080:80 run nginx 1 kube-nginx
kubecfg list /pods
```
