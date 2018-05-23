---
layout: 兰志远
title: hexo多台电脑更新博客
date: 2018-05-22 16:37:02
tags: hexo
type: "tags"
---
### 创建分支
* <label style="color:#b63650">hexo</label>生成的静态博客文件都是传到github上的，且默认放在master分支上，而配置文件都是放在本地的
* <label style="color:#b63650">hexo</label>(配置文件)都是可以放到hexo分支上(创建一个新的分支)，切换电脑时，直接git clone hexo分支

#### 在xxx.github.io仓库下创建一个新的hexo分支
切换到hexo分支，并在<label style="color:#b63650">->Settings->Branches->Default branch</label>中将默认分支设置为hexo，save保存
![](https://user-gold-cdn.xitu.io/2018/4/12/162b922ff0603fc4?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

#### 克隆hexo分支到本地
* 将新建的hexo分支克隆到本地，在终端中cd到xxx.github.io文件夹
* 使用<label style="color:#b63650">git branch</label>查看分支，应该默认是hexo

#### 部署文件
* 将本地的hexo配置文件(全部文件)全部拷贝到xxx.github.io文件根目录下
* 安装需要用到的插件(可选)

``` javascript
npm install hexo-generator-index --save
npm install hexo-generator-archive --save
npm install hexo-generator-category --save
npm install hexo-generator-tag --save
npm install hexo-server --save
npm install hexo-deployer-git --save
npm install hexo-deployer-heroku --save
npm install hexo-deployer-rsync --save
npm install hexo-deployer-openshift --save
npm install hexo-renderer-marked@0.2 --save
npm install hexo-renderer-stylus@0.2 --save
npm install hexo-generator-feed@1 --save
npm install hexo-generator-sitemap@1 --save
npm install hexo-generator-search --save
npm install hexo-generator-searchdb --save
```
* 将文件全部提交到hexo分支
* 注意事项
    1.主题文件夹下边可能会有<label style="color:#b63650">.git</label>、<label style="color:#b63650">.github</label>隐藏文件夹，将文件删除在提交，不然可能会提交不上去

> master分支和hexo分支各自保存着一个版本，master分支用于保存博客静态资源，提供博客页面供人访问；hexo分支用于备份博客部署文件，供自己维护更新，两者在一个GitHub仓库内也不会有任何冲突

### 在其他电脑更新博客
* 在新电脑克隆xxx.github.io仓库的hexo分支到本地
* cd到xxx.github.io文件夹下，执行npm install 
* 现在就可以在不同电脑下更新博客了