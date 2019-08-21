```
kubectl create -f kube-logging.yaml
```

```
kubectl get namespaces
```


# Step 2 — Creating the Elasticsearch StatefulSet
```

kubectl create -f elasticsearch_statefulset.yaml
```

```
kubectl rollout status sts/es-cluster --namespace=kube-logging

```

```
# kubectl port-forward es-cluster-0 9200:9200 --namespace=kube-logging

curl http://192.168.135.66:9200/_cluster/state?pretty

```

# Kibana

```
kubectl create -f kibana.yaml
```

```
kubectl rollout status deployment/kibana --namespace=kube-logging

```

```
kubectl get pods --namespace=kube-logging
```

```
http://192.168.135.66:32305

```

# fluentd
``` 
kubectl create -f fluentd.yaml
```

```
kubectl get ds --namespace=kube-logging
```


```
kubectl create -f counter.yaml
```
