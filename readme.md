# Ubuntu搭建NDS服务
## 安装dnsmasq服务
```
sudo apt install dnsmasq -y
#查看启动状态
sudo systemctl status dnsmasq
```
## 卸载系统自带的DNS服务
```
sudo systemctl stop systemd-resolved
sudo systemctl disable --now systemd-resolved
#备份/etc/resolv.conf
mkdir -p ~/bak
sudo mv /etc/resolv.conf  ~/bak/etc-resolv.conf
```
## 创建resolv.dnsmasq
sudo vim /etc/resolv.dnsmasq
```
nameserver 114.114.114.114
nameserver 8.8.8.8
```
这个文件配置上游dns，要不可能有些有些内网打不开
## 创建dnsmasqhosts
sudo vim /etc/dnsmasqhosts
```
192.168.1.148  admin.5188888.com
```
自定义host
## 编辑dnsmasq.conf
sudo vim /etc/dnsmasq.conf 编辑配置文件，把上面的两个文件配置到这个配置文件中
```
addn-hosts=/etc/dnsmasqhosts
resolv-file=/etc/resolv.dnsmasq
```
## 重启dnsmasq服务
```
sudo systemctl restart dnsmasq
sudo systemctl status dnsmasq
```