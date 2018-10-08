## Install OpenEBS

OpenEBS is a Container Attached Storage (CAS) that provides containerized block-storage for container environments such as Kubernetes, leveraging high availability and replication.

For more details, visit [openebs.io](https://docs.openebs.io/docs/next/conceptscas.html)

Kubecluster.io supports OpenEBS by default with any kubernetes deployment.

To install OpenEBS in a Kubecluster deployment, just run

````bash
helm install --namespace openebs --name openebs stable/openebs
````

That's it.

Your cluster now supports high available, replicated storage, backed by the Kubecluster.io node's RAID array.


#### Storage Classes

A storage (or multiple) storage class has to be created for OpenEBS.

````bash
kubectl apply -f https://raw.githubusercontent.com/openebs/openebs/v0.6/k8s/openebs-storageclasses.yaml  
````

This create some sample storage classes, feel free to create your own storage class where you refine the desired filesystem, replicas count, etc.