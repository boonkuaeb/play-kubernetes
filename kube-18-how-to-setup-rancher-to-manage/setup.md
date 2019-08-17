Rancher is tools for manage multi kubernetes cluster. I planed to
install Rancher in docker container and connect to Kubernetes cluster.

```
docker run -d --name rancher-server -v /tmp/rancher:/var/lib/rancher  --restart=unless-stopped -p 80:80 -p 443:443 rancher/rancher
```
