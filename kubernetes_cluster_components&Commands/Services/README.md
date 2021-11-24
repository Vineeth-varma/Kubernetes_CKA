## Service Info 
* Kubernetes Services enables communication between various components within and outside of the application.
## There are three types of services
### NodePort

* Where the service makes an internal POD accessible on a POD on the NODE.
* To access the application from CLI instead of web browser

  ```$ curl http://192.168.1.2:30008```

### ClusterIP
* In this case the service creates a Virtual IP inside the cluster to enable communication between different services such as a set of frontend servers to a set of backend servers.

### LoadBalancer
* Where the service provisions a loadbalancer for our application in supported cloud providers.
