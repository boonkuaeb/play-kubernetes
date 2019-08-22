# NFS
```
echo "[TASK 7] Start Create share directory"

mkdir -p /srv/nfs/kubedata/jfrog-postgresql
chown nfsnobody:nfsnobody /srv/nfs/kubedata/jfrog-postgresql
chmod 777 /srv/nfs/kubedata/jfrog-postgresql


cat >>/etc/exports<<EOF
/srv/nfs/kubedata/jfrog-postgresql      *(rw,sync,no_subtree_check,insecure)
EOF
exportfs -rav
exportfs -v
showmount -e



```

```
kubectl create -f 9-sts-pv.yaml

```
