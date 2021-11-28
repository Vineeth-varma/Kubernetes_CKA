## Backup And Restore Methods using etcd
* To make use of etcdctl for tasks such as back up and restore, make sure that you set the ETCDCTL_API to 3.  "export ETCDCTL_API=3"

**Backup:**
```
etcdctl snapshot save snapshot.db      # Useful to take snapshot and store in snapshot.db directory
etcdctl snapshot status snapshot.db    # To know the status
````
   **Complete Command:** 
```
ETCDCTL_API=3 etcdctl --endpoints=https://127.0.0.1:2379   
--cacert=/etc/kubernetes/pki/etcd/ca.crt   
--cert=/etc/kubernetes/pki/etcd/server.crt   
--key=/etc/kubernetes/pki/etcd/server.key  snapshot save /opt/snapshot-pre-boot.db
```
**Restore:** 
```
service kube-apiserver stop                                           # To restore stop the apiservice first
etcdctl snapshot restore snapshot.db --data-dir /var/lib/etcd-backup  # Restoring the data
```
* Once the data was restored, replace the --data-dir path with new restored directory "/var/lib/etcd-backup".
Then execute the below commands
```
    systemctl daemon-reload
    service etcd restart
    service kube-apiserver start.
```
**Complete Command:**
```
ETCDCTL_API=3 etcdctl  --data-dir /var/lib/etcd-from-backup snapshot restore /opt/snapshot-pre-boot.db
```
* As etcd is hosted as a static pod mention the path "/var/lib/etcd-from-backup" under volumes in /etc/kubernetes/manifests/etcd.

**Note**: To run etcdctl commands specify --endpoints, --cacert, --cert, --key of etcd server.
