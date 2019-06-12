---
layout: 兰志远
title: pm2进程管理工具
date: 2019-06-12 9:54:45
tags: node
type: "tags"
---
### pm2进程管理工具

安装

```
npm install pm2 -g  
```

启动

```
pm2 start app.js #启动一个进程
参数：
	--name myapp #设置进程名称为myapp
	--watch #监控进程，文件有变化自动重启进程
```

查看进程

```
pm2 list/pm2 status #进程列表
pm2 show id/pm2 info id #查看进程详细信息
```

停止

```
pm2 stop all #停止所有进程
pm2 stop id  #停止指定id的进程
```

重载

```
pm2 reload all #重载所有进程
pm2 reload id #重载指定id的进程
```

重启

```
pm2 restart all #重启所有进程
pm2 restart id #重启指定id的进程
```

查看日志

```
pm2 logs
```

