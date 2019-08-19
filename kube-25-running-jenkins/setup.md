# Install nfs first 

check storage class 
```
kubectl get storageclass
```
```
# Output
NAME                            PROVISIONER       AGE
managed-nfs-storage (default)   example.com/nfs   18h
```

# Config Jenkins


```
helm inspect values stable/jenkins > /tmp/jenkins.valuns
vim /tmp/jenkins.valuns
```

Update jenkins.valuns 
```
   adminUser: "admin"
   adminPassword: "password"
```


```
     limits:
       cpu: "500m"
       memory: "1024Mi"
```

```
   # Use ClusterIP if your setup includes ingress controller
   serviceType: NodePort
   nodePort: 32303
```

```
   ##   set, choosing the default provisioner.  (gp2 on AWS, standard on
   ##   GKE, AWS & OpenStack)
   ##
   storageClass: "managed-nfs-storage"
   annotations: {}
   accessMode: "ReadWriteOnce"
   size: "5Gi"

```
