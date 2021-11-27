## Cluster Upgrade Process
### OS Upgrades
* Whenever you would like to perform upgrades, maintainance activities or patches etc.., to a node - Then the pods on that node are not accessible

**Points to be noted:-** 
* When a pod is running without replicaSet on that node, then the kubelet waits for the node to come up for 5 mins after that time pod will be evicted. Which was set in 
  kube-controller-manager pod-eviction-timeout=5m0s..
* When pod is running with a relicaSet, it will be scheduled to some other active node.
* If you know that the node is going to come up in 5 mins then perform quick updates else use the below procedure:
```
kubectl drain node1                             # Which will Schedule everything to the other nodes.
kubectl drain node01 --ignore-daemonsets        # When you get a pop-up because of the presence of daemon set.
kubectl cordon node1                            # Which will just put some restriction on the node for schedulings not to happen.
kubectl uncordon node1                          # Apply this after updates are done and the node is ready for Scheduling.
```
### Cluster Upgrade Process
* For this upgrade process first try out using katakoda kubernetes playground

**kubeadm upgrade** - Google - You can find the procedure to upgrade components.  https://kubernetes.io/docs/tasks/administer-cluster/kubeadm/kubeadm-upgrade/
* Same process for both worker and master nodes but the upgrade process for worker has to be done by ssh into worker node.

**Note:** cordon,drain, uncordon commands have to be used in master node only for worker.
### Procedure:
**Master:**
```
kubectl drain controlplane/master 
kubeadm upgarde plan                    # It gives the versions available and other details related to upgarde process.

apt-mark unhold kubeadm &&                    
apt-get update && apt-get install -y kubeadm=1.20.0-00 &&   # Installing kubeadm package
apt-mark hold kubeadm

kubeadm version     
sudo kubeadm upgrade apply v1.20.0      (or)    apt install kubeadm=1.20.0-00

apt-mark unhold kubelet kubectl &&                           # kubelet & kubectl have to be installed seperately.
apt-get update && apt-get install -y kubelet=1.20.0-00 kubectl=1.20.0-00 && \     or  apt install kubelet=1.20.0-00
apt-mark hold kubelet kubectl

sudo systemctl daemon-reload
sudo systemctl restart kubelet
kubectl uncordon <node-to-drain>
```
