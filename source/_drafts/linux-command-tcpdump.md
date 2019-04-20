---
title: 使用tcpdump抓包
tags:
 - linux
 - 开发工具
category:
 - linux
 - 命令
---


<!-- more -->

[参考](https://www.zfl9.com/tcpdump.html)

## Flags意思
|TCP Flag|tcpdump Flag|解释|
|-------|---|-------|
|SYN    |S  |Syn数据包，会话建立请求|
|ACK    |A  |Ack数据包，确认发件人的数据|
|FIN    |F  |Finish结束标志，终止指示|
|RESET  |R  |Reset, 强制关闭连接|
|PUSH   |P  |Push，立即推送发件人的数据|
|URGENT |U  |Urgent，优先于其他数据|
|NONE   |.  |占位符，通常用于ACK|