## Service Info 
* Kubernetes Services enables communication between various components within and outside of the application.
* In Kubernetes, a Service is an abstraction which defines a logical set of Pods and a policy by which to access them.
* The set of Pods targeted by a Service is usually determined by a selector.
### Services without Selectors
* You want to have an external database cluster in production, but in your test environment you use your own databases.
* You want to point your Service to a Service in a different Namespace or on another cluster.  
* You are migrating a workload to Kubernetes. While evaluating the approach, you run only a portion of your backends in Kubernetes.
* In all the above cases you can define a Service without a Pod selector,
 
```
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  ports:
    - protocol: TCP
      port: 80
      targetPort: 9376
  ```
* Because this Service has no selector, the corresponding Endpoints object is not created automatically. You can manually map the Service to the network address and port where it's running, by adding an Endpoints object manually:
```
apiVersion: v1
kind: Endpoints
metadata:
  name: my-service
subsets:
  - addresses:
      - ip: 192.0.2.42
    ports:
      - port: 9376
```

## There are three types of services
### NodePort

* Where the service makes an internal POD accessible on a POD on the NODE.
* To access the application from CLI instead of web browser

  ```$ curl http://192.168.1.2:30008```

### ClusterIP
* In this case the service creates a Virtual IP inside the cluster to enable communication between different services such as a set of frontend servers to a set of backend servers.

### LoadBalancer
* Where the service provisions a loadbalancer for our application in supported cloud providers.
