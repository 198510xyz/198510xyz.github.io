# OpenVZ上安装bbr脚本

## CentOS 6 升级glibc

如果是CentOS 6，需要先升级glibc到2.14以上（CentOS 7不需要）：

```
wget https://cloud.ktsee.eu.org/201709/glibc-215.rpms.zip
unzip glibc-215.rpms.zip
rpm -Fhv *.rpm
```
然后执行`ldd --version`，如果版本是2.15表示升级完成

## 安装BBR

已测试通过的系统： Ubuntu 14.04 x64、Ubuntu 16.04 x64、CentOS 6 x64、CentOS 7 x64 只支持 64 位系统，要求 glibc 版本 2.14 以上。

```
wget https://raw.githubusercontent.com/198510xyz/shell-scripts/master/ovz-bbr/ovz-bbr-installer.sh
chmod +x ovz-bbr-installer.sh
./ovz-bbr-installer.sh
```

需要配置的有如下几个选项：

1. 需要加速的端口，即的 SS 端口。加速开启之后，流量会先经过 BBR 处理，之后再发送给后端的 SS。
2. 可能需要配置 “公网接口名称”，即你服务器上具有公网 IP 的接口名称。搬瓦工 OpenVZ 上默认都是 venet0，但是有朋友可能需要安装在其他服务器上，所以我加入了此选项。

需要注意的是，在有 firewalld 的服务器上安装的时候，firewalld 会干扰 iptables 的规则，造成网络不通（现在具体原因未知，谁有解决方案可以提示一下）。所以在装有 firewalld 的服务器上需要先退出 firewalld：

```
systemctl disable firewalld
systemctl stop firewalld
```

如需卸载，请使用：

```
./ovz-bbr-installer.sh uninstall
```

## 判断 BBR 已正常工作

判断 bbr 是否正常启动可以尝试 `ping 10.0.0.2`，如果能通，说明 bbr 已经启动。

然后检查 iptables 规则

```
iptables -t nat -nL
Chain PREROUTING (policy ACCEPT)
target     prot opt source               destination
LKL_IN     all  --  0.0.0.0/0            0.0.0.0/0
 
Chain POSTROUTING (policy ACCEPT)
target     prot opt source               destination
 
Chain OUTPUT (policy ACCEPT)
target     prot opt source               destination
 
Chain LKL_IN (1 references)
target     prot opt source               destination
DNAT       tcp  --  0.0.0.0/0            0.0.0.0/0            tcp dpt:8989 to:10.0.0.2
```

里边会看到多了一张链表 LKL_IN，里边有相应的端口规则。 
