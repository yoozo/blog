---
title: 常用的工具代理配置
tags:
  - git
  - docker
  - npm
category:
  - 环境配置
  - 代理
date: 2019-04-03 23:14:47
---

因为众所周知的原因，很多开发工具需要代理才能正常使用。
<!-- more -->

## Git
### 设置代理
```bash
git config --global http.proxy http://127.0.0.1:1080
git config --global http.proxy http://127.0.0.1:1080
git config --global http.proxy socks5://127.0.0.1:1080
git config --global https.proxy socks5://127.0.0.1:1080
```

### 取消代理 
```bash
git config --global --unset http.proxy
git config --global --unset https.proxy
```

## docker for windows
### 设置镜像
为了永久性保留更改，您可以修改 /etc/docker/daemon.json 文件并添加上 registry-mirrors 键值。
```
{"registry-mirrors": ["https://registry.docker-cn.com"]}
```

## npm
### 临时使用
```bash
npm --registry https://registry.npm.taobao.org install <package>
```

### 持久使用
```bash
npm config set registry https://registry.npm.taobao.org

# 配置后可通过下面方式来验证是否成功
npm config get registry
```

### 通过cnpm使用
```bash
npm install -g cnpm --registry=https://registry.npm.taobao.org
```
### 设置代理
```
npm config set proxy http://server:port
npm config set https-proxy http://server:port
```