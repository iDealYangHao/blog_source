---
title: AWS搭建VPS
date: 2022-02-02 11:22:09
tags: VPN
categories: Tools
---

# 远程登陆AWS
下载的一个密钥xxx.pem,我直接放在Downloads里面在，需要先给这个文件降权限，从0644降到0600
``` 
chmod 0600 ~/Downloads/xxx.pem    //降权
ssh -i ~/Downloads/xxx.pem ubuntu@192.100.0.1   //登陆
```
<!--more-->
# 安装ss
```
//下载脚本
sudo wget –no-check-certificate -O shadowsocks.sh https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks.sh

//提权，使其可执行
sudo chmod +x shadowsocks.sh

//运行脚本
sudo ./shadowsocks.sh
```
选择加密方式时，建议选择**aes-256-cfb**

# 加速
```
sudo wget --no-check-certificate https://github.com/teddysun/across/raw/master/bbr.sh

sudo chmod +x bbr.sh

sudo ./bbr.sh
```

各种版本的shadowsocket客户端地址： https://shadowsocks.org/en/download/clients.html



