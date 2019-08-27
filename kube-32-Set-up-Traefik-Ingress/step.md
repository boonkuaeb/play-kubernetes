# Set HA Proxy
```
yum install -y haproxy
```

```
vi /etc/haproxy/haproxy.cfg
```

Remove every thing after front ` maxconn 3000`
```
frontend http_front
  bind *:80
  stats uri /haproxy?stats
  default_backend http_back

backend http_back
  balance roundrobin
  server kube <worker-node1-ip>:80
  server kube <worker-node2-ip>:80


```

```
systemctl enable haproxy
systemctl start haproxy
systemctl status haproxy

```

# Install traefik Ingress Controller

[install Ingress Controllers](https://docs.traefik.io/user-guide/kubernetes/)
[examples k8s ](https://github.com/containous/traefik/tree/v1.7/examples/k8s)

```
kubectl apply -f https://raw.githubusercontent.com/containous/traefik/v1.7/examples/k8s/traefik-rbac.yaml
```

```
kubectl describe clusterrole traefik-ingress-controller -n kube-system
```

```
kubectl apply -f https://raw.githubusercontent.com/containous/traefik/v1.7/examples/k8s/ui.yaml
```

### Deploy daemon set 
```
kubectl apply -f https://raw.githubusercontent.com/containous/traefik/v1.7/examples/k8s/traefik-ds.yaml
```
```
kubectl get all -n kube-system | grep traefik
```



# Deploy sample Application
```
kubectl create namespace demo-traefik
```

```
kubectl apply -f nginx-deploy-blue.yaml -f nginx-deploy-green.yaml -f nginx-deploy-main.yaml -f backofspring.yaml --namespace demo-traefik
```

# Create ingress service
```
kubectl apply -f ingress-resource.yaml --namespace demo-traefik
```

```
kubectl get ing --namespace demo-traefik && kubectl describe ing ingress-resource --namespace demo-traefik
```

```
kubectl expose deployment bankofspring-deployment --port=80 --target-port=8080 --namespace demo-traefik 

kubectl expose deployment nginx-blue-deployment --port=80 --target-port=80 --namespace demo-traefik

kubectl expose deployment nginx-green-deployment --port=80 --target-port=80 --namespace demo-traefik

kubectl expose deployment nginx-main-deployment --port=80 --target-port=80 --namespace demo-traefik


```


```
kubectl get ing --namespace demo-traefik && kubectl describe ing ingress-resource --namespace demo-traefik

```

















