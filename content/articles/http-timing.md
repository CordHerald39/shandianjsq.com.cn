---
title: "网页慢在 DNS、连接还是首字节：用 curl 分段记录"
category: "tutorials"
label: "实用教学"
description: "网页慢在 DNS、连接还是首字节：用 curl 分段记录，按步骤核对条件、错误与恢复方法。"
date: "2026-10-04"
updated: "2026-10-04"
author: "闪电加速器中文资料编辑"
draft: false
---

## 从一次请求取得分段时间
不要只用“打开很慢”描述问题。先关闭大文件下载，保持设备、接入网络和测试目标一致。以下是 Windows PowerShell 的示意命令，并非本站测量结果：
`curl.exe -o NUL -sS --max-time 20 -w 'dns=%{time_namelookup} connect=%{time_connect} tls=%{time_appconnect} first=%{time_starttransfer} total=%{time_total}' https://example.com/`
## 数值是累计时间
这些时间以秒为单位，连接、TLS、首字节和总时间通常从请求开始累计，不能把它们当作互不相干的独立耗时后相加。代理方式、连接复用、重定向都会影响解释；通过代理时，连接阶段可能反映的是代理端点连接。
## 建立能复查的记录
连续记录三次，同表保存时间、客户端模式、节点标签、目标和错误码。偶发一次变慢先重试，不据此排速度排名。总时间很长但首字节较快，可继续检查响应体大小和传输过程；首字节很晚，则把连接与应用响应分开调查。不要把服务端等待全部归因于本地节点。
## 来源与继续阅读
[curl 官方 write-out 手册](https://curl.se/docs/manpage.html)解释各变量。[节点与速度检查](/network/)说明测试条件的固定方法。
