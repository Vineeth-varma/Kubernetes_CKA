## Namespace Info
* We have created Objects such as PODs, Deployments and Services in our cluster. Whatever we have been doing we have been doing in a NAMESPACE.
* There will always be one namespace in kubernetes which is **"default"**. It is automatically created when kubernetes is setup initially.
* To create a Namespace.

  ```kubectl create namespace dev```

* By default, we will be in a default namespace. To switch to a particular namespace permenently run the below command.

  ```kubectl config set-context $(kubectl config current-context) --namespace=dev```

* To view pods in all namespaces

  ```kubectl get pods --all-namespaces```

* To limit resources in a namespace, create a resource quota. To create one start with **"ResourceQuota"** definition file.
