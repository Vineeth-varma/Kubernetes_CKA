### Monitor cluster Components
* We can monitor with the help of cAdviser present in kubelet which sends metrics to "Metric Server".
* https://github.com/kubernetes-sigs/metrics-server/releases  - Metric server can be downloaded from here.
* View the cluster performance ```kubectl top node```
* View performance metrics of pod  ```kubectl top pod```
### Managing Application Logs:
* To view the logs```kubectl logs -f event-simulator-pod```
* If there are multiple containers in a pod then you must specify the name of the container explicitly in the command.
```
kubectl logs -f <pod-name> <container-name>
kubectl logs -f even-simulator-pod event-simulator
```
