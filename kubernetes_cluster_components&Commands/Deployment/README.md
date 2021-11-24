## Deployment Yaml file and Info

* A Deployment named nginx-deployment is created, when you use the above yaml file.
* The Deployment creates three replicated Pods, indicated by the .spec.replicas field.
* The .spec.selector field defines how the Deployment finds which Pods to manage. 

**Commands**  
* Create the deployment using deployment definition file

  ```kubectl create -f deployment-definition.yaml```

* The deployment automatically creates a ReplicaSet. To see the replicasets

  ```kubectl get replicaset```

* The replicasets ultimately creates PODs. To see the PODs
  
  ```kubectl get pods```

* To see the Deployment rollout status, run 
  
  ```kubectl rollout status deployment/nginx-deployment.```

* To see the labels automatically generated for each Pod, run 
   
   ```kubectl get pods --show-labels```
 
**Follow the steps given below to update your Deployment:**
* Let's update the nginx Pods to use the nginx:1.16.1 image instead of the nginx:1.14.2 image.
  
  ```kubectl set image deployment/nginx-deployment nginx=nginx:1.16.1```

* Alternatively, you can edit the Deployment and change 
  
  ```kubectl edit deployment/nginx-deployment```
  
* Run ```kubectl get rs``` to see that the Deployment updated the Pods by creating a new ReplicaSet and scaling it up to 3 replicas, as well as scaling down the old ReplicaSet to 0 replicas.
* Deployment ensures that only a certain number of Pods are down while they are being updated. By default, it ensures that at least 75% of the desired number of Pods are up (25% max unavailable).

* Checking rollout history of a deployment

  ```kubectl rollout history deployment/nginx-deployment```

* Now you've decided to undo the current rollout and rollback to the previous revision:
 
  ```kubectl rollout undo deployment/nginx-deployment```

* Alternatively, you can rollback to a specific revision by specifying it with --to-revision:

  ```kubectl rollout undo deployment/nginx-deployment --to-revision=2```
  
* You can scale a Deployment by using the following command:

  ```kubectl scale deployment/nginx-deployment --replicas=10```
  
* Assuming horizontal Pod autoscaling is enabled in your cluster, you can setup an autoscaler for your Deployment and choose the minimum and maximum number of Pods you want to run based on the CPU utilization of your existing Pods.

   ```kubectl autoscale deployment/nginx-deployment --min=10 --max=15 --cpu-percent=80```
   
* Watch the status of the rollout until it's done.

   ```kubectl get rs -w```
   

