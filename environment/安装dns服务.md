# 安装dns服务

这里我们需要提供一套dns用作域名解析，如果内部环境已经有dns服务可以跳过此步骤。可以使用轻量级的dnsmasq来解决此问题，安装配置如下：

```bash
# yum install dnsmasq
# chkconfig dnsmasq on
```

安装好以后需要增加hosts.conf配置文件，这里假设新增的域名是```osinstall.idcos.net```，ip地址是```10.0.1.1```

```bash
# cat /etc/dnsmasq.conf
conf-dir=/etc/dnsmasq.d

# cat /etc/dnsmasq.d/hosts.conf
address=/osinstall.idcos.net/10.0.1.1
```
