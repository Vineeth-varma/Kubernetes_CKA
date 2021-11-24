## Deployment Yaml file and Info

**Commands**
* Create the deployment using deployment definition file
```kubectl create -f deployment-definition.yaml```
* The deployment automatically creates a ReplicaSet. To see the replicasets
```kubectl get replicaset```
* The replicasets ultimately creates PODs. To see the PODs
```kubectl get pods```
