# Provision Dynamic NFS

1. Edit deployment.yaml file 
   -  replace your NFS server IP
   
2. Edit Class.yaml 
   -  Change a Storage-Class-Name 
   ```
    apiVersion: storage.k8s.io/v1
    kind: StorageClass
    metadata:
      name: managed-nfs-storage
      annotations:
        storageclass.kubernetes.io/is-default-class: "true"
    provisioner: example.com/nfs
    parameters:
      archiveOnDelete: "false"
   ```
3. Run command 
    ```
    kubectl apply -f rbac.yaml -f class.yaml -f deployment.yaml 
    
    ```
# Add Helm and Tiller
1. Create namespace
``` 
kubectl -n kube-system create serviceaccount tiller
```
2. Create clusterrolebindign 
```
kubectl create clusterrolebinding tiller --clusterrole cluster-admin --serviceaccount=kube-system:tiller 
```
3. Create Tiller 
```
helm init --service-account tiller
```

# Install Prometheus 
```
helm inspect values stable/prometheus > ./prometheus.values
```

`vi /tmp/prometheus.values` to edit 
- edit `type: NodePort`
- add `nodePort: 32301`
```
     ## List of IP addresses at which the Prometheus server service is available
     ## Ref: https://kubernetes.io/docs/user-guide/services/#external-ips
     ##
     externalIPs: []

     loadBalancerIP: ""
     loadBalancerSourceRanges: []
     servicePort: 80
     nodePort: 32301
     type: NodePort

```

```
helm install stable/prometheus --name prometheus --values /tmp/prometheus.values --namespace prometheus
```

# Install Grafana
```
helm inspect values stable/grafana > /tmp/grafana.values
```
`vi /tmp/grafana.values` to edit 
- edit `type: NodePort`

```
## ref: http://kubernetes.io/docs/user-guide/services/
 ##
 service:
   type: NodePort
   nodePort: 32302
   port: 80

```
- set admin password 
```
 # Administrator credentials when not using an existing secret (see below)
 adminUser: admin
 adminPassword: password
```

- Eanble persistence 
```
 persistence:
   enabled: true
   # storageClassName: default
```

```

# helm install stable/grafana --name grafana --values /tmp/grafana.values --namespace grafana

helm install -f grafana.yml charts/stable/grafana --name grafana --namespace grafana
```


## Issue : grafana with persistence not working with nfs
```
helm install -f grafana.yml charts/stable/grafana --name grafana --namespace grafana

```

