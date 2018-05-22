---
layout: 兰志远
title: 使用github搭建hexo个人博客
date: 2018-05-22 11:53:49
tags: hexo
---
### 准备工作
* 1.准备一个github账号，没有的话去[github](https://github.com/)注册
* 2.电脑安装node、git、npm

### 安装hexo
* 当node、git都安装完成之后，在终端运行如下命令：
``` javascript
npm install -g hexo 
```
### 开始搭建
* 1.在电脑中新建一个空文件夹，名字随意，如MyBlog
* 2.cd到当前文件夹
* 3.在终端运行如下命令，生成模板
``` javascript
hexo init
```
##### 安装完模板应该会有一个package.json文件，执行如下命令安装依赖：
``` javascript
npm install 
```
##### 然后运行如下命令开始hexo服务器:
``` javascript
hexo s
```
##### 输入[http://localhost:4000/](http://localhost:4000/)，应该就可以看到以下页面
![](http://upload-images.jianshu.io/upload_images/4122543-dfe49f13bcfd743d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/600)
### 关联github
#### 新建一个github仓库
* 在github上创建名字为XXX.github.io的项目，xxx必须是自己github账号的用户名

#### 修改<label style="color:#b63650">_fonfig.yml</label>配置文件
* 1.打开本地MyBlog根目录下边的_fonfig.yml配置文件
* 2.将其中的type设置为git，repository是你github.io仓库的地址
* 3.每次个属性冒号后边都要加一个空格，不然会报错
``` javascript
deploy:
  type: git
  repository: https://github.com/CoderTitan/CoderTitan.github.io.git
  branch: master
```
#### 将配置文件部署到github上
* 打开终端，cd到MyBlog文件夹下，执行如下命令

##### 在MyBlog根目录下执行如下命令生成静态文件：
``` javascript
hexo generate     或者：hexo g
```
##### 此时若出现如下报错：
``` javascript
ERROR Local hexo not found in ~/blog
ERROR Try runing: 'npm install hexo --save'
```
##### 则执行命令：
``` javascript
npm install hexo --save
```
##### 再执行配置命令：
``` javascript
hexo deploy           或者：hexo d
```
##### 报错一: 若执行命令hexo deploy仍然报错：无法连接git或找不到git，则执行如下命令来安装hexo-deployer-git：
``` javascript
npm install hexo-deployer-git --save
```
##### 报错二: 若执行命令hexo d报以下错误:
``` javascript
ERROR Plugin load failed: hexo-server
//或者类似的错误
ERROR Plugin load failed: hexo-renderer-sass
```
##### 则执行响应的命令:
``` javascript
sudo npm install hexo-server
//或者
sudo npm install hexo-renderer-sass
```
##### 最后执行：
``` javascript
hexo d
```
* hexo d执行完成后，在浏览器打开http://xxx.github.io就能看到搭建好的博客了

### 安装主题
* 我们可以去[官方网站](https://hexo.io/themes/)下载主题
* 示例next

#### cd到MyBlog根目录下执行
``` javascript
git clone https://github.com/theme-next/hexo-theme-next themes/next
```
下载的主题默认是在theme文件夹下，然后重新执行hexo g来生成

#### 每次部署文章的步骤
``` javascript
hexo clean           //清除缓存文件 (db.json) 和已生成的静态文件 (public)

hexo g             //生成缓存和静态文件
 
hexo d             //重新部署到服务器
```
### 域名绑定
* 现在使用的域名是Github提供的二级域名XXX.github.io，也可以绑定为自己的个性域名
* 可以到阿里万网购买，可以直接在网站做域名解析

### 域名解析
如果将域名指向一个域名，实现与被指向域名相同的访问效果，需要增加CNAME记录。登录万网，在你购买的域名后边点击：解析, 如下图
![](http://upload-images.jianshu.io/upload_images/4122543-952aa0a8a84a089f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
进入解析页面后点击添加解析, 向你的 DNS 配置中添加 3 条记录, 如下图
注意CNAME记录添加的是username.github.io.(不要忘记后面的.), 可能最后一个点不显示(我的就不显示)
![](http://upload-images.jianshu.io/upload_images/4122543-b2435667d603f844.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 设置github配置信息
* 打开你的xxx.github.io项目地址，找到设置页面
* 滚动到下方找到github pages模块，在custom domain，输入你购买的域名，点击save保存

### 创建CNAME文件
* 在/MyBlog/themes/landscape/source目录下新建文件名为：CNAME文件，注意没有后缀名！直接将自己的域名写入
* CNAME一定要大写
* 完成上述步骤后, 终端cd到MyBlog目录下执行如下命令重新部署：
* 最后, 等十分钟左右，刷新浏览器，用你自己域名访问下试试

``` javascript
hexo clean

hexo g

hexo d
```


