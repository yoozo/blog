---
title: centos7.3下搭建 lnmp 环境
date: 2019-04-02 22:52:25
tags: 
 - php
 - mysql
 - nginx
category: 环境配置
---

如何在centos7.3 下搭建好php的web开发环境

## yum安装nginx最新稳定版本

### 配置nginx yum存储库
创建/etc/yum.repos.d/nginx.repo 文件，添加以下代码 
```conf
    [nginx]
    name=nginx repo
    baseurl=http://nginx.org/packages/OS/OSRELEASE/$basearch/
    gpgcheck=0
    enabled=1
```
 <!-- more -->

然后还要修改baseurl参数
 >OS: rhel 或 centos
 >OSRELEASE: 6 或 7

因为我现在的系统是centos7.3所以要将baseurl修改为`http://nginx.org/packages/centos/7/$basearch/`，修改后
```conf
    [nginx]
    name=nginx repo
    baseurl=http://nginx.org/packages/centos/7/$basearch/
    gpgcheck=0
    enabled=1
```

### 安装nginx
通过以下命令安装nginx，运行命令 `yum install nginx`

### 开启nginx服务
使用以下命令启动nginx `service nginx start`

您可以使用以下命令检查nginx的状态 `service nginx status`

## yum安装MySQL5.7最新版本
参考资料:[mysql官方文档][1]

### 配置MySQL yum存储库
1. 转至MySQL开发人员专区中的“[下载MySQL Yum存储库][2]”页面。
2. 选择并下载适用于您的平台的发行，这里我们选择**Red Hat Enterprise Linux 7 / Oracle Linux 7 (Architecture Independent), RPM Package**，点击**Download**。
3. 在下载页面获取下载地址。
   ![copy_url.png][3] 
   >这里我获取到的地址是`https://dev.mysql.com/get/mysql57-community-release-el7-11.noarch.rpm`
4. 使用以下命令安装下载的发行包，替换 **platform-and-version-specific-package-name** 为下载的RPM包的名称：
    yum localinstall platform-and-version-specific-package-name.rpm
  >按照以上步骤，最终要运行的`yum localinstall https://dev.mysql.com/get/mysql57-community-release-el7-11.noarch.rpm`

### 安装MySQL
通过以下命令安装MySQL `yum install mysql-community-server`

### 启动MySQL服务
使用以下命令启动MySQL服务 `service mysqld start`

您可以使用以下命令检查MySQL服务的状态 `service mysqld status`

## php7.2源码安装
如果需要yum安装的可以看 [这里][4]

### 准备工作
去[php官网][5]下载php-7.2.1.tar.gz，然后把压缩包放在/home目录下，并解压到当前目录下。
解压php-7.2.1.tar.gz

```bash
cd /home
tar zxvf php-7.2.1.tar.gz
```


## 编译安装
以下命令默认在解压后的目录文件中操作
>`cd /home/php-7.2.1`

1. 修改编译配置*configure*，我这里选择的配置如下
    ```conf
    ./configure \
    --prefix=/usr/local/php72 \
    --enable-fpm \
    --with-curl \
    --with-freetype-dir \
    --with-gd \
    --with-gettext \
    --with-iconv-dir \
    --with-kerberos \
    --with-libdir=lib64 \
    --with-libxml-dir \
    --with-mysqli \
    --with-openssl \
    --with-pcre-regex \
    --with-pdo-mysql \
    --with-pdo-sqlite \
    --with-pear \
    --with-png-dir \
    --with-xmlrpc \
    --with-xsl \
    --with-zlib \
    --enable-bcmath \
    --enable-libxml \
    --enable-inline-optimization \
    --enable-mbregex \
    --enable-mbstring \
    --enable-opcache \
    --enable-pcntl \
    --enable-shmop \
    --enable-soap \
    --enable-sockets \
    --enable-sysvsem \
    --enable-xml \
    --enable-zip
    ```
   因为要在nginx下运行，所以配置要默认编译生成php-fpm，所以需要 `--enable-fpm`
   另外我希望将php7.2相关的文件放在 **/usr/local/php72** 目录下`--prefix=/usr/local/php72`
   其他配置可以根据需要进行选择，查看配置帮助 `./configure --help`
2. 配置完成之后就可以进行编译和安装了
    ```bash
    make
    make install
    ```
   安装成功后会多了 **/usr/local/php72**
3. 创建软连接
    ```bash
    #为php-fpm创建软连接
    ln -s /usr/local/php72/sbin/php-fpm /usr/local/sbin/php-fpm
    #为php创建软连接
    ln -s /usr/local/php72/bin/php /usr/local/bin/php
    ```
4. 创建php-fpm服务
   为了更加方便操作php-fpm，创建服务可以看 [这里][6]

## 构建lnmp
根据前面的步骤安装好所有需要的软件之后就可以


  [1]: https://dev.mysql.com/doc/refman/5.7/en/linux-installation-yum-repo.html
  [2]: http://dev.mysql.com/downloads/repo/yum/
  [3]: /images/1783506500.png
  [4]: https://webtatic.com/
  [5]: http://php.net/downloads.php
  [6]: http://www.yoozo.xin/archives/16.html