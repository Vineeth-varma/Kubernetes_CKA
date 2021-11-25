## Commands for Scheduling pods to nodes   
**Labels & Selectors**
* ```kubectl get po --show-labels ```          It shows all the labels attached to a pod.
* ```kubectl get all --show-labels ```         It shows all the labels in a default namespace.
* ````kubectl get po -l app=app1 ```            Use 'l-flag' to know which pod is using a particualr label.
* ```kubectl get pods --selector env=dev ```   It displays the pods with that label or selector.

**Taints & Tolerations**
* ```kubectl taint nodes <node-name> key=value:taint-effect```  Command to taint a node 
* ```kubectl taint nodes node1 app=blue:NoSchedule```   Example 
* ```kubectl taint nodes <node-name> app=blue:NoSchedule-  ```       That '-' symbol at the end is to untaint a node.
* ```kubectl explain pod --recursive | less    ```                 Which shows the complete pod Parameters
* ```kubectl explain pod --recursive | grep -A5 tolerations  ```    After tolerations it will show the next 5 lines
* Add the below toleration under spec to make the node accept pod scheduling
```
spec:
  tolerations:
  - key: "app"
    operator: "Equal"
    value: "blue"
    effect: "NoSchedule"
   ```
   
**Node Selector**
* ```kubectl label nodes <node-name> <label-key>=<label-value>```
* ```kubectl label nodes node-1 size=Large```  We can label the nodes and those we can use to schedule using node selectors.
```
spec: 
 nodeSelector:
  size: Large
```
  
**Node Affinity**
* The primary feature of Node Affinity is to ensure that the pods are hosted on particular nodes.
* A combination of taints and tolerations and node affinity rules can be used together to completely dedicate nodes for specific parts.
```
spec:
 containers:
 - name: data-processor
   image: data-processor
 affinity:
   nodeAffinity:
     requiredDuringSchedulingIgnoredDuringExecution:
        nodeSelectorTerms:
        - matchExpressions:
          - key: size
            operator: In
            values: 
            - Large
            - Medium
 affinity:
   nodeAffinity:
     requiredDuringSchedulingIgnoredDuringExecution:
        nodeSelectorTerms:
        - matchExpressions:
          - key: size
            operator: NotIn
            values: 
            - Small
 affinity:
   nodeAffinity:
     requiredDuringSchedulingIgnoredDuringExecution:
        nodeSelectorTerms:
        - matchExpressions:
          - key: size
            operator: Exists
```
 
**Static Pods**
* Without kubernetes master component we can create pods in worker node with the help of kubelet.
* You can configure the kubelet to read the pod definition files from a directory on the server designated to store information about pods.
* The designated directory can be any directory on the host and the location of that directory is passed in to the kubelet as an option while running the service.
* The option is named as --pod-manifest-path.
* Mostly people use this directory **/etc/kubernetes/manifests** to store the required files.
* Instead of specifying the option directly in the kubelet.service file, you could provide a path to another config file using the config option --config,
  and define the directory path as staticPodPath in the file.
* To view the static pods
```
docker ps
kubectl get pods -A | grep "-nodename"   # To check the no.of static pods which will attached by nodename
```
* To Identify the Static pod location
```
ps -aux | grep kubelet                  # identify the config file 
--config=/var/lib/kubelet/config.yaml   # Then check in the config file for staticPodPath.
```
Example for creating a static pod in config directory of staticPods.
```
kubectl run --restart=Never --image=busybox static-busybox --dry-run=client -o yaml --command -- sleep 1000 > /etc/kubernetes/manifests/static-busybox.yaml
```
