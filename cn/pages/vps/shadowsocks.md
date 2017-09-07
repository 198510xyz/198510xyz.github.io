# 影梭安装

## Windows安装服务端

1. 下载最新的[shadowsocks-libqss](https://github.com/shadowsocks/libQtShadowsocks/releases)（Fedora下软件包名为shadowsocks-libQtShadowsocks）
2. 准备好config.json文件（[范例文件点此](https://github.com/shadowsocks/libQtShadowsocks/blob/master/shadowsocks-libqss/config.json)，点Raw另存为config.json就能下载下来了），server字段填写”0.0.0.0″（如果走IPv6线路，填”::”），加密方式可以改成更新潮的”chacha20″（老旧的Shadowsocks客户端可能不支持chacha20加密）
3. 要shadowsocks-libqss.exe以server mode运行需要加上-S参数，你可以从命令行提示符去运行。或者，更简单的，把下面的代码保存为bat脚本shadowsocks-server.bat
4. 将shadowsocks-server.bat与shadowsocks-libqss.exe, config.json放在同一个文件夹下，执行shadowsocks-server.bat即可

```
::This batch will run shadowsocks-libqss in server mode using the config.json file in current folder as the configuration

@echo off
::this script is updated for version 1.7.0
shadowsocks-libqss.exe -c config.json -S
```

## Linux安装服务端

### CentOS源安装

下载[Fedora Copr](https://copr.fedorainfracloud.org/coprs/librehat/shadowsocks/)并且放置到/etc/yum.repos.d/，然后通过yum安装：

```
yum update
yum install shadowsocks-libev
```

安装完成后，需要调整config.json中的server字段为”0.0.0.0″（如果走IPv6线路，填”::”）

## 安装客户端
- Mac平台: [ShadowsocksX-NG](https://github.com/shadowsocks/ShadowsocksX-NG/releases)
- Win平台：[shadowsocks-windows](https://github.com/shadowsocks/shadowsocks-windows/releases)
