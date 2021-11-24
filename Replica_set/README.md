## ReplicSet Yaml and Info
* ReplicaSet you no need to create it gets created automatically with Deployment.

### Difference between ReplicaSet and Replication Controller
* Replication Controller is the older technology that is being replaced by a ReplicaSet.
* ReplicaSet is the new way to setup replication.

**Note:** Carefully observe we are giving Labels to pod spec and the same labels we are creating as selectors in ReplicaSet spec.

**Commnads**
* To Create the replication controller
```kubectl create -f replicaset-definition.yaml```
* To list all the replication controllers
```kubectl get replicaset```
* To list pods that are launch by the replication controller
```kubectl get pods```
