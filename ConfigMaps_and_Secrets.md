## Basic Usage of Configmaps and Secrets in Kubernetes

### ConfigMaps:
ConfigMaps Usage in Various ways

* **Using Imperative Command**
```
kubectl create configmap <configmap-name> --from-literal=<key>=<value>
kubectl create configmap <configmap-name> --from-file=<path_to_the_file>   # When you have more key-value pairs store in one file and specify the file path.
```
 * **You can reference in the pod-definition file under spec using this**
```
envFrom:
- configMapRef:
    name: <configMap-name>    
```     
* **We can also do the above with the help of Volumes.**
```
volumes:
  name: configmap-volume
  configMap:
    name: <configMap-name>    
 ```
* The above three mentioned methods we can use to pass certain configuration using configMaps.

### Secrets:
Secrets usage in various ways

* **Using Imperative commands, In Imperative approach automatically the values will get encoded.**
```
kubectl create secret generic <secret-name> --from-literal=<key>=<value>
kubectl create secret generic <secret-name> --frrom-file=<path_to_the_file>
```
* **For decletrative approach use "echo -n "string" | base64" command.**

* **You can reference in the pod-definition file under spec using this.**
```
envFrom:
  secretRef:
    name: <secret_name>
```
* **We can also do the above with the help of Volumes.**
```
    volumeMounts:
    - name: foo
      mountPath: "/etc/foo"

volumes:
  - name: foo
    secret:
      secretName: mysecret
      items:
      - key: username
        path: my-group/my-username  # username secret is stored under /etc/foo/my-group/my-username file instead of /etc/foo/username.
```        
