# ubuntu配置终端clash

## 下载

[clash](https://github.com/Dreamacro/clash/releases)下载最新版本

```sh
gunzip clash # 解压以及重命名
mkdir /root/.config/clash && mv clash /root/.config/clash/clash && cd /root/.config/clash # 移动到指定目录
wget -O config.yaml url # 下载配置文件
```

## 配置文件

默认生成的配置文件在用户home目录下的.config/clash目录下

```yaml
log-level: info
mode: Global
# RESTful API 口令
secret: 'password'
allow-lan: true
```

配置好之后到[clash配置地址](https://clash.razord.top/)配置

输入要配置的机器的公网ip，端口默认为9090，密钥和配置文件的secret一致

之后在网页的代理里面选择节点

## 配置终端映射

```
export http_proxy=http://127.0.0.1:7890
export https_proxy=http://127.0.0.1:7890
# 直接映射全部
export all_proxy=http://127.0.0.1:7890
```

```sh
# 添加到常用的shell启动脚本
alias proxy="export all_proxy=http://127.0.0.1:7890"
alias unproxy="unset all_proxy"
alias clash-start="systemctl start clash"
alias clash-stop="systemctl stop clash"
alias clash-status="systemctl status clash"
```

## 设置系统服务

/etc/systemd/system/clash.service

```sh
[Unit]
Description=clash-core
[Service]
Type=simple
ExecStart=/root/.config/clash/clash -f /root/.config/clash/config.yaml
```

```sh
systemctl daemon-reload # 重新加载系统服务命令
systemctl start clash
systemctl status clash
systemctl stop clash
```

## docker启动代理

```sh
docker run --env ALL_PROXY="http://127.0.0.1:代理端口" --network host -ti image:tag /bin/bash
```