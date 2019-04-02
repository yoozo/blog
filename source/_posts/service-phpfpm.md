---
title: 将php-fpm加入服务
date: 2019-04-02 23:44:34
tags: php
category: 环境配置
---

源码安装的php是不带service启动脚本的，要是想用`service php-fpm start`这类命令的话需要自行配置。
<!-- more -->

前提
========================
 - php源码安装的目录为***/usr/local/php72***
 - php-fpm.conf里的`pid = run/php-fpm.pid`这句代码没被注释，如果被注释先去掉前面的分号`;`

添加php-fpm系统服务
========================
新建php-fpm文件
-----------------------
新建文件：***/etc/init.d/php-fpm*** ，添加以下代码
>注意:代码中的`PHPDIR`，请修改为自己的php源码安装的目录

    #! /bin/sh
    # Comments to support chkconfig on CentOS
    # chkconfig: 2345 65 37
    #
    set -e
    
    PHPDIR=/usr/local/php72
    PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin
    DESC="php-fpm daemon"
    NAME=php-fpm
    DAEMON=$PHPDIR/sbin/$NAME
     
    CONFIGFILE=$PHPDIR/etc/php-fpm.conf
    PIDFILE=$PHPDIR/var/run/$NAME.pid
    SCRIPTNAME=/etc/init.d/$NAME
     
    # Gracefully exit if the package has been removed.
    test -x $DAEMON || exit 0
     
    d_start() {
      $DAEMON -y $CONFIGFILE || echo -n " already running"
    }
     
    d_stop() {
      kill -QUIT `cat $PIDFILE` || echo -n " not running"
    }
     
    d_reload() {
      kill -HUP `cat $PIDFILE` || echo -n " can't reload"
    }
     
    case "$1" in
      start)
            echo -n "Starting $DESC is success"
            d_start
            echo "."
            ;;
      stop)
            echo -n "Stopping $DESC is success"
            d_stop
            echo "."
            ;;
      reload)
            echo -n "Reloading $DESC configuration..."
            d_reload
            echo "reloaded."
      ;;
      restart)
            echo -n "Restarting $DESC is success"
            d_stop
            sleep 1
            d_start
            echo "."
            ;;
      *)
             echo "Usage: $SCRIPTNAME {start|stop|restart|force-reload}" >&2
             exit 3
            ;;
    esac

添加可执行权限
----------------------------------
`chmod +x /etc/init.d/php-fpm`

结束语
==================================
至此，已经可以用一下命令来开启php-fpm了
开机启动：`chkconfig php-fpm on`
启动服务：`service php-fpm start`
停止服务：`service php-fpm stop`
重启服务：`service php-fpm reload`


