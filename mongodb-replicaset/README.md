### MongoDB replica set
##### How to deploy a High Available MongoDB ReplicaSet cluster on Kubernetes using helm 

This guide assumes that you already have a Kubernetes cluster with 3 nodes: node1,node2,node3. 

If you don't already have one, please visit [KubeCluster.io](https://kubecluster.io) to get a Kubernetes cluster up and running.

**1. Persistent storage**

We're going to use replicated block-storage provided by OpenEBS.

To setup OpenEBS please follow [our guide](../openebs).

We will be using the `openebs-mongodb` StorageClass created as part of the guide.


**2. Install via Helm chart**

If you don't already have helm, just run `helm init`.
```bash
helm install --name my-db -f ./values.yml stable/mongodb-replicaset
```

In our case, the MongoDB URI will be: `mongodb://my-db-mongodb-replicaset-0.my-db-mongodb-replicaset.default.svc.cluster.local:27017`

Note: adjust the StorageClass and ./values.yml to set the desired volume size and replication count.
