1. Install InfluxDB ( Matrix collection ) 
   -  influxdb.yaml 
      - pod
      - service
      - namespace is `kube-system` 
   - run command 
   ```
   kubectl create -f influxdb.yaml
   ```
2. Create ServiceAccount
   -  heapster.yaml
      - ServiceAccount name heapster
      - ClusterRoleBinding ( Binding heapster ServiceAccount to
        cluster-adin role )
      - Pod 
      - Service
   - Run Command 
   ```
   kubectl create -f heapster.yaml
   ```
   
   ```
   kubectl -n kube-system get pods -o wide
   ```
3. dashboard.yaml 
   -  create Secret call `kubebernetes-dashboard-certs`
   - create ServiceAccount call `kubebernetes-dashboard`
   - create Role call `kubebernetes-dashboard-minimal`. This role just
     define. What the user can do ?
   - create RoleBinding 
   - Deployment
   - Service
   
   
   ```
   kubectl create -f dashboard.yaml
   ```
   
   ```
   kubectl -n kube-system get pods -o wide
   
   ```
   
   ```
   kubectl cluster-info
   ```
   
4. sa_cluster_admin.yaml
   -  create ServiceAccount call  dashboard-admin


   ```
   kubectl create -f sa_cluster_admin.yaml
   ```
   
   To get the secret 
   ```
   kubectl describe sa dashboard-admin -n kube-system
   ```
   Copy the secret and run command below
   
   ```
   kubectl describe secret {secret_name} -n kube-system
   ```
