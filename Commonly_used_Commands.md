## Commnds Used to play with Kubernetes Resources and Objects

### Commonly used Commnads
* ```kubectl get po,deploy,cm,secret,rs,sts,...```      To get a kubernetes resource
* ```kubectl get all```                                 To get all thresources in default namespace 
* ```kubectl get po -A```                               To get all the pods in a default namespace 
* ```kubectl describe po/deploy/cm/secret.......```     To describe a resource
* ```kubectl logs```                                    To view logs, used for pods
* ```kubectl delete po/deploy/cm/secret.......```       To delete a resource
* ```kubectl edit po/deploy/cm/secret....... ```        To edit a resource 
* ```kubectl apply -f definition-file.yaml```          To update changes to a resource yaml file
* ```kubectl create -f definition-file.yaml```          To create a resource using yaml file
* ```kubectl replace -f definition-file.yaml```        To replace the yaml file 

### Imerative commands
* ```kubectl run nginx --image nginx ```                              To create a pod
* ```kubectl run nginx --image=nginx --dry-run=client -o yaml ```     Generate Pod YAML Manifest file.
* ```kubectl run nginx --image=nginx --port=80 --expose```            Crating Pod along with service.
* ```kubectl expose pod redis --port=6379 --name redis-service```    Creating a service for pod.
* ```kubectl scale --replicas=6 -f replicaset-definition.yaml```      To edit/modify replicas

**For Deployments**
* ```kubectl create deployment --image=nginx nginx```
* ````kubectl create deployment --image=nginx nginx --dry-run=client -o yaml```
* ```kubectl create deployment --image=nginx nginx --replicas=4 --dry-run=client -o yaml > nginx-deployment.yaml ```` 
* ```kubectl rollout restart deployment <deployment-name>```              For restarting the deployment
* ```kubectl set image deployment nginx nginx=nginx:1.18 ```                Updating the image version in deployment.
* ```kubectl expose pod <pod_name> --port=6379 --name redis-service --dry-run=client -o yaml```     Here pod labels will be attached to the service
* ```kubectl create service clusterip redis --tcp=6379:6379 --dry-run=client -o yaml ``` This will not generate correct pod labels, modify once the service file is created.
* ```kubectl expose pod nginx --port=80 --name nginx-service --type=NodePort --dry-run=client -o yaml```     Type Nodeport
