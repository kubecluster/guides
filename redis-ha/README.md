### Redis HA with Redis Sentinel
##### How to deploy a High Available Redis Sentinel cluster on Kubernetes using helm

This guide assumes that you already have a Kubernetes cluster.

If you don't already have one, please visit [KubeCluster.io](https://kubecluster.io) to get a Kubernetes cluster up and running.

**Install via Helm chart**

If you don't already have helm, just run `helm init`.

This guide will install a cluster with 3 replicas of redis-server and redis-sentinel. For customizations you can change the values.yml file.
```aidl
helm install --name my-redis-cluster -f ./values.yml stable/redis-ha
```

In our case, the Redis URI will be accessible with the following configuration
* master: `mymaster`
* nodes: `my-redis-cluster-redis-ha-sentinel.default.svc.cluster.local:26379`
