---
layout:     post
title:      "Docker remote api"
subtitle:   "Docker Remote api"
date:       2016-02-03 12:00:00
author:     "Sriram Mantha"
---

Docker exposes remote api and they can be pretty handy to get some good information. They can be especially useful when you have a swarm cluster. Swarm distributes services across the nodes in the cluster. The swarm api can useful for querying cluster status across different nodes.

## Enabling docker remote api in RHEL

1. Add a file

```
/etc/systemd/system/docker.service.d
```

2. Add entry to expose the docker remote api ports

```
[Service]
ExecStart=
ExecStart=/usr/bin/dockerd -H tcp://0.0.0.0:2376 -H unix:///var/run/docker.sock
```

3. Reload the deamon file
```
sudo systemctl daemon-reload
```

4. Restart docker

```
sudo systemctl restart docker
```

5. Verify if its working by querying the version resource

```

[root@i]# curl -X GET http://localhost:2376/version
{
  "Version":"1.12.1","ApiVersion":"1.24","GitCommit":"23cf638","GoVersion":"go1.6.3","Os":"linux","Arch":"amd64","KernelVersion":"3.10.0-327.28.3.el7.x86_64"
}

```
