---
title: linux命令 - firewall-cmd修改防火墙配置
date: 2020-03-15 12:53:09
tags:
  - linux
category:
  - linux
  - 命令
---


firewall-cmd管理防火墙常用到的配置

## 状态选项
```bash
--state                   返回并打印防火墙状态
--reload                  重新加载防火墙并保留状态信息
--check-config            检查永久配置是否有错误
--list-all-zones          列出为所有区域添加或启用的所有内容
--list-all                列出为当前所在区域添加或启用的所有内容
```
<!-- more -->
例子：重启防火墙`firewall-cmd --reload`

## 配置选项
```bash
--permanent                                     设置一个永久选项
--add-port=<portid>[-<portid>]/<protocol>       配置允许通过的端口
--add-service=service                           配置允许通过的服务
```
例子：配置一个永久允许通过的端口3306`firewall-cmd --permanent --add-port=3306/tcp`
