## Imperative Commands for all kinds of Kubernetes resources:
### Commonly used commands for any resource
```
kubectl get po,deploy,cm,secret,rs,sts,... 
kubectl get all
kubectl get po -A
kubectl describe po/deploy/cm/secret.......
kubectl logs   - Only used for pods
kubectl delete po/deploy/cm/secret.......
kubectl edit po/deploy/cm/secret.......
kubectl apply -f definition-file.yaml
kubectl create -f definition-file.yaml
kubectl replace-f definition-file.yaml
```

### To deploy a docker container by creating a POD.
```
kubectl run nginx --image nginx
kubectl run nginx --image=nginx --dry-run=client -o yaml  # For sample dry run, Generate Pod YAML Manifest file.
kubectl run nginx --image=nginx --port=80 --expose         # Crating Pod along with service.
kubectl expose pod redis --port=6379 --name redis-service   # Creating a service for pod.
```
* One way is just edit replicas and update to 6 in Yaml definition file
* Second way is to use kubectl scale command.

  ```kubectl scale --replicas=6 -f replicaset-definition.yaml```

### Creating Deployment
```
kubectl create deployment --image=nginx nginx
kubectl create deployment --image=nginx nginx --dry-run=client -o yaml
kubectl create deployment --image=nginx nginx --replicas=4 --dry-run=client -o yaml > nginx-deployment.yaml  
```
### Some more useful Commands
```
kubectl rollout restart deployment <deployment-name>  # For restarting the deployment
kubectl set image deployment nginx nginx=nginx:1.18    # Updating the image version in deployment.
kubectl expose pod <pod_name> --port=6379 --name redis-service --dry-run=client -o yaml    # Here pod labels will be attached to the service
kubectl create service clusterip redis --tcp=6379:6379 --dry-run=client -o yaml    # This will not generate correct pod labels, modify once the service file is created.
kubectl expose pod nginx --port=80 --name nginx-service --type=NodePort --dry-run=client -o yaml    # Type Nodeport
```
