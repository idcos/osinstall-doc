# 安装http服务

系统安装所需要的镜像源使用http的方式来提供，需要安装nginx并下载安装介质然后导入ISO文件生成安装源。

```bash
# rpm -ivh http://nginx.org/packages/centos/6/noarch/RPMS/nginx-release-centos-6-0.el6.ngx.noarch.rpm
# yum install nginx
# chkconfig nginx on
```

下载系统安装介质，以centos 6.7为例，需要下载ISO文件并导入http目录。

```bash
# mkdir -p /home/www/iso /home/www/centos/6.7/os/x86_64/
# wget -c -P /home/www/iso http://mirrors.aliyun.com/centos/6.7/isos/x86_64/CentOS-6.7-x86_64-bin-DVD1.iso
# mount -o loop /home/www/iso/CentOS-6.7-x86_64-bin-DVD1.iso /media
# rsync -az /media/ /home/www/centos/6.7/os/x86_64/
# umount /media
```
