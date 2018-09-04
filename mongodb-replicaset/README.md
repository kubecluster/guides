### MongoDB replica set
##### How to deploy a High Available MongoDB ReplicaSet cluster on Kubernetes using helm 

This guide assumes that you already have a Kubernetes cluster with 3 nodes: node1,node2,node3. 

If you don't already have one, please visit [KubeCluster.io](https://kubecluster.io) to get a Kubernetes cluster up and running.

**1. Persistent storage**

We're going to use PersistentVolumes so that our data is persisted on the Node even if the container is deleted.

The volumes are declared in the `pv.yml` file. As KubeCluster.io is using bare-metal nodes, we have to
make use of the local storage drives of the servers. To achieve this, we're going to use the `hostPath` type of PersistentVolumes
and we're going to create enough volumes on each node so that Kubernetes will eventually bind them to our containers. This guide
creates 3 volumes (1 on each node), assuming your cluster consists of 3 worker nodes and you are deploying a replica set of 3 mongodb instances.

First, create the StorageClass if you did not create it already:
```
kubectl create -f ./storageclass.yml
```

Then create the PersistentVolumes

```
kubectl create -f ./pv.yml
``` 

**2. Install via Helm chart**

If you don't already have helm, just run `helm init`.
```aidl
helm install --name my-db -f ./values.yml stable/mongodb-replicaset
```

In our case, the MongoDB URI will be: `mongodb://my-db-mongodb-replicaset-0.my-db-mongodb-replicaset.default.svc.cluster.local:27017`

