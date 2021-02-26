# Why backup etcd?

Etcd is the backend data storage solution for K8s clusters. So all the K8s objects, applications and configurations are stored in this etcd.

Therefore you will likely want to be able to back up your cluster's data by backing up the etcd.

## Backing up etcd.

You can back up etcd data using the etcd command line tool, **etcdctl** 

So we can use etcdtl snapshot save command to back up the data.

````
ETCDTL_API=3 etcdtl --endpoints $ENDPOINT snapshot save <file name>
````

## Restoring etcd

You can restore etcd data from a backup using the etcdtl snapshot restore command.
You will need to supply some additional parameters as the restore operations creates a new logical cluster. 

````
ETCDTL_API=3 etcdtl snapshot restore <file name>
````
