# Kubernetes Administration Documentation
## Certification Details
* Certified Kubernetes Administrator  - https://www.cncf.io/certification/cka/
* Exam Circullum Topics   - https://github.com/cncf/curriculum
* Candidate Handbook  - https://www.cncf.io/certification/candidate-handbook
* Exam Tips   - http://training.linuxfoundation.org/go//Important-Tips-CKA-CKAD
* Use the code - **DEVOPS15** - while registering for the CKA or CKAD exams at Linux Foundation to get a 15% discount.
* https://github.com/kodekloudhub/certified-kubernetes-administrator-course  - For more CKA info from mumshad.

## Kubernetes Architecture
**ETCD Cluster** 
* It is a key value database store which stores all the nodes info.
* The ETCD Datastore stores information regarding the cluster such as Nodes, PODS, Configs, Secrets, Accounts, Roles, Bindings and Others.
* Every information you see when you run the kubectl get command is from the ETCD Server.

**Kube-apiserver**   
* Kube-apiserver is the primary component in kubernetes.
* Kube-apiserver is responsible for authenticating, validating requests, retrieving and Updating data in ETCD key-value store.
* In fact kube-apiserver is the only component that interacts directly to the etcd datastore. 
* The other components such as kube-scheduler, kube-controller-manager and kubelet uses the API-Server to update in the cluster in their respective areas.

**Control Manager** 
* Kube Controller Manager manages various controllers in kubernetes.
* In kubernetes terms, a controller is a process that continuously monitors the state of the components within the system and works towards bringing the whole system to the desired functioning state.
* **Node Controller**  - Responsible for monitoring the state of the Nodes and taking necessary actions to keep the application running.
* **Replication Controller**  - Responsible for monitoring the status of replicasets and ensuring that the desired number of pods are available at all time within the set.
* There are many more such controllers available within kubernetes like Deployment Controller, Node Controller, Namespace Controller, Endpoint Controller, PV-Binder, PV-Protection controllers etc...,
**Kube-Scheduler** 
* kube-scheduler is responsible for scheduling pods on nodes.
* The kube-scheduler is only responsible for deciding which pod goes on which node. It doesn't actually place the pod on the nodes, that's the job of the kubelet.
**Kubelet** 
* Kubelet is the sole point of contact for the kubernetes cluster.
* The kubelet will create the pods on the nodes, the scheduler only decides which pods goes where.
**Kubeproxy**
* Within Kubernetes Cluster, every pod can reach every other pod, this is accomplish by deploying a pod networking cluster to the cluster.
* Kube-Proxy is a process that runs on each node in the kubernetes cluster.
