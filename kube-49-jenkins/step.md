```
docker run -d -p 5000:5000 --restart=always --name registry -v docker:/var/lib/registry registry:2
```

```
helm search jenkins
```

```
helm inspect values stable/jenkins > ./jenkins.values
```

Edit contain


```
ssh root@kworker1
```

```
chmod 666 /var/run/docker.sock
```

Set Local registry to kworker1 ` vi /etc/docker/daemon.json`
```
{
    "insecure-registries": ["172.42.42.1:5000"]
}
```

```
systemctl reload docker
exit
```

