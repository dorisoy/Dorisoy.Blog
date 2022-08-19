---
title: 宝塔安装mysql后使用navicat连接
date: 2021-01-24 15:10:22
tags:
  - 服务器搭建
categories:
  - 部署
permalink: /pages/1ac16a/
sidebar: auto
author:
  name: dorisoy
  link: https://github.com/gezhicui
---

今天自己买了个服务器折腾，在服务器中创建完数据库后，本地使用`navicat`无法连接到数据库，在这记录一下解决方法

### 基础配置

#### 宝塔面板 => 放行端口:3306

![](https://yangblogimg.oss-cn-hangzhou.aliyuncs.com/blogImg/放行端口.png)

#### 2.阿里云安全组 => 放行端口:3306

![](https://yangblogimg.oss-cn-hangzhou.aliyuncs.com/blogImg/1238941-20190418094559780-716689832.png)

![](https://yangblogimg.oss-cn-hangzhou.aliyuncs.com/blogImg/1238941-20190418094439006-1724183264.png)

![](https://yangblogimg.oss-cn-hangzhou.aliyuncs.com/blogImg/1238941-20190418094903913-1417230784.png)

### 远程连接方式配置

第一种：

#### 通过宝塔面板 phpMyAdmin

![](https://yangblogimg.oss-cn-hangzhou.aliyuncs.com/blogImg/1238941-20190418095310063-2039931197.png)

#### 面板 phpMyAdmin 操作

![](https://yangblogimg.oss-cn-hangzhou.aliyuncs.com/blogImg/1238941-20190418095751279-1585934843.png)

![](https://yangblogimg.oss-cn-hangzhou.aliyuncs.com/blogImg/1238941-20190418095919907-668358998.png)

#### 在光标处输入如下命令

```sql
-- 选择你要操作的数据库
use mysql；

-- 给root账户授权（root默认只有本机访问的权限，要通过其他机器访问，必须授权）
GRANT ALL PRIVILEGES ON *.* TO'root'@'%' IDENTIFIED BY 'root' WITH GRANT OPTION;

-- 最后刷新数据库服务
flush privileges;
```

命令执行：`Ctrl + Enter`

这样，我们再通过`navicat`就可以连接到远程服务器上的数据库了

---

还有第二种配置，不过我没成功，先贴出来：

#### 权限管理

在宝塔面板找到你的数据库管理面板，找到你要远程访问的数据库选择权限管理=>选择所有人或（如果有独立 IP 可以选择指定 IP 访问）=>点击提交

![](https://yangblogimg.oss-cn-hangzhou.aliyuncs.com/blogImg/1238941-20190826093542176-849388633.png)

![](https://yangblogimg.oss-cn-hangzhou.aliyuncs.com/blogImg/1238941-20190826093658600-2121359886.png)

![](https://yangblogimg.oss-cn-hangzhou.aliyuncs.com/blogImg/1238941-20190826094146198-173346913.png)

#### navicat 连接

![](https://yangblogimg.oss-cn-hangzhou.aliyuncs.com/blogImg/1238941-20190826094238577-714789314.png)

![](https://yangblogimg.oss-cn-hangzhou.aliyuncs.com/blogImg/1238941-20190826094708779-549641841.png)
