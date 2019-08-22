1. Creat NFS server by vagrant 
```

echo "[TASK 7] Enable and Start NFS service"
systemctl enable nfs-server.service
systemctl start nfs-server.service

echo "[TASK 7] Start Create share directory"
mkdir -p /srv/nfs/kubedata-app-alpha/alp-app-prometheus-server
chown nfsnobody:nfsnobody /srv/nfs/kubedata-app-alpha
chmod 777 /srv/nfs/kubedata-app-alpha/alp-app-prometheus-server
cat >>/etc/exports<<EOF
/srv/nfs/kubedata-app-alpha/alp-app-prometheus-server       *(rw,sync,no_subtree_check,insecure)
EOF
exportfs -rav
exportfs -v
showmount -e


```


2. ssh to kworker1 and kworker2 terminal

3. run command 
```
mount -t nfs 172.42.42.200:/srv/nfs/kubedata-app-alpha/alp-app-prometheus-alertmanager/prometheus-server /mnt
```
