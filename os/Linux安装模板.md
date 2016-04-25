# Linux安装模板

这里以CentOS 6.7系统为例，简单介绍一下kickstart的使用方法。

```bash
install
url --url=http://osinstall.idcos.com/centos/6.7/os/x86_64/
lang en_US.UTF-8
keyboard us
network --onboot yes --device bootif --bootproto dhcp --noipv6
rootpw  --iscrypted $6$eAdCfx9hZjVMqyS6$BYIbEu4zeKp0KLnz8rLMdU7sQ5o4hQRv55o151iLX7s2kSq.5RVsteGWJlpPMqIRJ8.WUcbZC3duqX0Rt3unK/
firewall --disabled
authconfig --enableshadow --passalgo=sha512
selinux --disabled
timezone Asia/Shanghai
text
reboot
zerombr
bootloader --location=mbr --append="console=tty0 biosdevname=0 audit=0 selinux=0"
clearpart --all --initlabel
part /boot --fstype=ext4 --size=256 --ondisk=sda
part swap --size=2048 --ondisk=sda
part / --fstype=ext4 --size=100 --grow --ondisk=sda

%packages --ignoremissing
@base
@core
@development

%pre
_sn=$(dmidecode -s system-serial-number 2>/dev/null | awk '/^[^#]/ { print $1 }')
curl -H "Content-Type: application/json" -X POST -d "{\"Sn\":\"$_sn\",\"Title\":\"启动OS安装程序\",\"InstallProgress\":0.6,\"InstallLog\":\"SW5zdGFsbCBPUwo=\"}" http://osinstall.idcos.com/api/osinstall/v1/report/deviceInstallInfo
curl -H "Content-Type: application/json" -X POST -d "{\"Sn\":\"$_sn\",\"Title\":\"分区并安装软件包\",\"InstallProgress\":0.7,\"InstallLog\":\"SW5zdGFsbCBPUwo=\"}" http://osinstall.idcos.com/api/osinstall/v1/report/deviceInstallInfo

%post
progress() {
    curl -H "Content-Type: application/json" -X POST -d "{\"Sn\":\"$_sn\",\"Title\":\"$1\",\"InstallProgress\":$2,\"InstallLog\":\"$3\"}" http://osinstall.idcos.com/api/osinstall/v1/report/deviceInstallInfo
}

_sn=$(dmidecode -s system-serial-number 2>/dev/null | awk '/^[^#]/ { print $1 }')

progress "配置主机名和网络" 0.8 "Y29uZmlnIG5ldHdvcmsK"

# config network
cat > /etc/modprobe.d/disable_ipv6.conf <<EOF
install ipv6 /bin/true
EOF

curl -o /tmp/networkinfo "http://osinstall.idcos.com/api/osinstall/v1/device/getNetworkBySn?sn=${_sn}&type=raw"
source /tmp/networkinfo

cat > /etc/sysconfig/network <<EOF
NETWORKING=yes
HOSTNAME=$HOSTNAME
GATEWAY=$GATEWAY
NOZEROCONF=yes
NETWORKING_IPV6=no
IPV6INIT=no
PEERNTP=no
EOF

cat > /etc/sysconfig/network-scripts/ifcfg-eth0 <<EOF
DEVICE=eth0
BOOTPROTO=static
IPADDR=$IPADDR
NETMASK=$NETMASK
ONBOOT=yes
TYPE=Ethernet
NM_CONTROLLED=no
EOF

progress "添加用户" 0.85 "YWRkIHVzZXIgeXVuamkK"
useradd yunji

progress "配置系统服务" 0.9 "Y29uZmlnIHN5c3RlbSBzZXJ2aWNlCg=="

# config service
service=(crond network ntpd rsyslog sshd sysstat)
chkconfig --list | awk '{ print $1 }' | xargs -n1 -I@ chkconfig @ off
echo ${service[@]} | xargs -n1 | xargs -I@ chkconfig @ on

progress "调整系统参数" 0.95 "Y29uZmlnIGJhc2ggcHJvbXB0Cg=="

# custom bash prompt
cat >> /etc/profile <<'EOF'

export LANG=en_US.UTF8
export PS1='\n\e[1;37m[\e[m\e[1;32m\u\e[m\e[1;33m@\e[m\e[1;35m\H\e[m:\e[4m`pwd`\e[m\e[1;37m]\e[m\e[1;36m\e[m\n\$ '
export HISTTIMEFORMAT='[%F %T] '
EOF

progress "安装完成" 1 "aW5zdGFsbCBmaW5pc2hlZAo="
```

说明：

* `url --url=xxx` 设定安装http镜像源，请根据实际情况修改
* `rootpw  --iscrypted` 这里指定的是加密后的密码`yunjikeji`，我们强烈建议用户使用加密的密码，密码加密字符串请使用`grub-crypt`生成
* 在进入安装界面的时候，请根据参考规范使用`curl`上传消息和进度，通知server端目前的状态
* 在完成分区和安装软件包以后，运行`post`脚本的时候，请使用`progress`函数上传消息和进度
* 网络配置请根据api接口查询，并通过脚本的方式来配置，默认只支持单个ip的配置，不支持多ip获取
* 在安装配置完成以后，确保上传进度为`1`，这样server端会记录服务器已经安装完成并删除pxe安装文件
