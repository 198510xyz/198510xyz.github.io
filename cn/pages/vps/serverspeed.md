# 锐速安装

## Linux安装锐速

### 使用锐速安装脚本
```
wget --no-check-certificate -qO /tmp/appex.sh "https://raw.githubusercontent.com/0oVicero0/serverSpeeder_Install/master/appex.sh" && bash /tmp/appex.sh 'install'
```
如果不能匹配到内核，按以下操作：

 - 通过 uname -r 查看到的版本号为 2.6.32-642.el6.x86_64 ,
 - 去查看 [锐速版本库](https://github.com/0oVicero0/serverSpeeder_kernel/blob/master/serverSpeeder.txt) 发现有个内核版本很接近 2.6.32-573.1.1.el6.x86_64 .
 - 执行安装命令:
```
wget --no-check-certificate -O appex.sh https://raw.githubusercontent.com/0oVicero0/serverSpeeder_Install/master/appex.sh && chmod +x appex.sh && bash appex.sh install '2.6.32-573.1.1.el6.x86_64'
```
完成安装

### 阻止CentOS升级内核以防锐速失效

修改`/etc/yum.conf`，在 [main] 的最后添加：

```
#禁止更新内核
exclude=kernel*
```

### OpenVZ架构无法安装锐速的解决

安装bbr

## Windows安装锐速

下载[Windows版的serverSpeeder](https://moeclub.org/attachment/WindowsScript/serverSpeeder_v3.11.12.3_UI3.7.20.0_Win_All.zip),安装目录下双击运行serverSpeeder.bat即可使用.可根据自身情况自行更改最后几行批处理命令.(不用管.reg文件,bat会帮你自动执行.)
