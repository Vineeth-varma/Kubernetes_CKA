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

### HeadLess Service
* Sometimes you don't need load-balancing and a single Service IP. In this case, you can create what are termed "headless" Services, by explicitly specifying "None" for the cluster IP (.spec.clusterIP).

### ClusterIP
* Exposes the Service on a cluster-internal IP. Choosing this value makes the Service only reachable from within the cluster. This is the default ServiceType.
### NodePort
* Exposes the Service on each Node's IP at a static port (the NodePort). A ClusterIP Service, to which the NodePort Service routes, is automatically created. You'll be able to contact the NodePort Service, from outside the cluster, by requesting <NodeIP>:<NodePort>.
* Service node port range --service-node-port-range flag (default: 30000-32767).
### LoadBalancer
* Exposes the Service externally using a cloud provider's load balancer. NodePort and ClusterIP Services, to which the external load balancer routes, are automatically created.
### ExternalName
* Maps the Service to the contents of the externalName field (e.g. foo.bar.example.com), by returning a CNAME record with its value. No proxying of any kind is set up. 
### Ingress
* You can also use Ingress to expose your Service. Ingress is not a Service type, but it acts as the entry point for your cluster. It lets you consolidate your routing rules into a single resource as it can expose multiple services under the same IP address
