---
title: 开启VPS的bbr for debian9
date: 2017-09-22 16:32:04
tags: [debian, VPS]
categories: linux
---
`仅适用于新开的 KVM/XEN/Hyper-V VPS，root 环境。`

### 1、更新系统

依次执行以下几条命令：

```shell
apt-get update  
apt-get upgrade  
apt-get dist-upgrade 
```

然后重启一次 VPS

`reboot`


### 2.开启 BBR

由于 Debian9 默认的内核就是 4.9 且编译了 TCP BBR 的内容，所以可以直接通过参数开启 BBR

```shell
echo "net.core.default_qdisc=fq" >> /etc/sysctl.conf
echo "net.ipv4.tcp_congestion_control=bbr" >> /etc/sysctl.conf
```

保存生效

```shell
sysctl -p
```

执行
```shell
sysctl net.ipv4.tcp_available_congestion_control
```

如果结果是这样

`net.ipv4.tcp_available_congestion_control = bbr cubic reno`

就开启了。


-----------
如果系统为debian 8 ，要先更新系统 到debian9再执行上述操作

### 1、替换 sources.list 源文件

Debian 8 代号 Jessie ，我们需要替换 /etc/apt/sources.list 里的源为 Debian 9 的代号 Stretch

备份一下原来的文件
```shell
cp -r /etc/apt/sources.list /etc/apt/sources.list.old  
```
然后直接替换
```shell
sed -i 's/jessie/stretch/g' /etc/apt/sources.list 
```
### 2、更新系统

还是老步骤，建议一步一步来
```shell
apt-get update  
apt-get upgrade  
```
### 3、升级系统

```shell
apt-get dist-upgrade  
```
重启一次
```shell
reboot
```
更新完系统之后，就可以直接开启bbr了

`参考` [将 Debian 8 升级至 9 并开启 BBR](https://yjk.im/debian-8-to-9/)