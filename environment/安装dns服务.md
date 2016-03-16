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
address=/osinstall/10.0.1.1
address=/osinstall.idcos.net/10.0.1.1
```

修改完成以后，启动dnsmasq服务，测试域名是否生效

```bash
# service dnsmasq start
# dig @127.0.0.1 osinstall.idcos.net A

; <<>> DiG 9.8.2rc1-RedHat-9.8.2-0.30.rc1.el6_6.3 <<>> osinstall.idcos.net @127.0.0.1
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 13030
;; flags: qr aa rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 0

;; QUESTION SECTION:
;osinstall.idcos.net.           IN      A

;; ANSWER SECTION:
osinstall.idcos.net.    0       IN      A       10.0.1.1

;; Query time: 0 msec
;; SERVER: 127.0.0.1#53(127.0.0.1)
;; WHEN: Tue Mar  1 14:44:16 2016
;; MSG SIZE  rcvd: 53
```
