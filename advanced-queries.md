# Queries in Kubernetes with Json Paths

**Get the list of nodes in JSON format**
```
kubectl get nodes -o json
```

**Get the details of the node <node-name> in json format**
```
kubectl get node <node-name> -o json
```

**Use JSON PATH query to fetch node names**
```
kubectl get nodes -o=jsonpath='{.items[*].metadata.name}'
```

**Use JSON PATH query to retrieve the osImages of all the nodes**
```
kubectl get nodes -o jsonpath='{.items[*].status.nodeInfo.osImage}'
```

**Get the users in a kube-config file**
```
kubectl config view --kubeconfig=my-kube-config  -o jsonpath="{.users[*].name}"
```

**A set of Persistent Volumes are available. Sort them based on their capacity**
```
kubectl get pv --sort-by=.spec.capacity.storage
```

**Retrieve just the first 2 columns of output**
```
kubectl get pv --sort-by=.spec.capacity.storage -o=custom-columns=NAME:.metadata.name,CAPACITY:.spec.capacity.storage
```

**Use a JSON PATH query to identify the context configured for the `aws-user` in the `my-kube-config` context file**
```
kubectl config view --kubeconfig=my-kube-config -o jsonpath="{.contexts[?(@.context.user=='aws-user')].name}"
```


**EXAM**
```
k get deploy -n admin2406 -o=custom-columns=DEPLOYMENT:.metadata.name,CONTAINER_IMAGE:.spec.template.spec.containers[*].image,READY_REPLICAS:.spec.replicas,NAMESPACE:.metadata.namespace
```