---
title: docker
date: 2019-01-31 17:39:40
tags:
categories:
---

# docker 简单使用

## 配置 Docker

因为国内访问 Docker Hub 较慢, 可以使用腾讯云提供的国内镜像源, 加速访问 Docker Hub

依次执行以下命令

```bash
echo "OPTIONS='--registry-mirror=https://mirror.ccs.tencentyun.com'" >> /etc/sysconfig/docker
```

```
systemctl daemon-reload
```

```
service docker restart
```

