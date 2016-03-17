---
layout: default
title: 安装Jekyll并部署到github
category: tech
tags: [jekyll, github.io, pages.github]
---

这篇文章主要包括一下内容

- 安装Jekyll
	+ 安装ruby
    + 安装DevKit
    + 安装jekyll
- 运行Jekyll
    + 搭建项目框架
    + 编写第一篇文章
    + 预览
- 发布到github
    + 新建github仓库
    + 同步代码
    + 在github.io上面预览
- 部署到自己的域名

### 安装Jekyll

#### 安装ruby

1. [下载ruby的安装包,这里是64位的链接](http://dl.bintray.com/oneclick/rubyinstaller/rubyinstaller-2.2.4-x64.exe)
2. 下载完成之后直接安装,全部默认安装,最后装完之后目录在`C:\Ruby22-x64`,下面会用到
3. 一切安装顺利,在我的电脑上并没有遇到什么困难

#### 安装DevKit

1. [下载DevKit的安装包](http://dl.bintray.com/oneclick/rubyinstaller/DevKit-mingw64-64-4.7.2-20130224-1432-sfx.exe)
2. 下载完成之后直接安装,安装过程需要选择一个目录来解压文件,这里选用c:/DevKit目录,主要是避免中文路径或者包含空格的路径可能导致的未知问题
3. `win+R` 输入`cmd`按`回车`打开命令提示符
4. 输入以下

{% highlight sh %}
cd c:\DevKit
ruby dk.rb init
echo "- C:\Ruby22-x64" >> config.yml
ruby dk.rb review
ruby dk.rb install
{% endhighlight %}

**此时ruby和gem(gem相对于ruby可以认为是npm相对于nodejs)都已经装好**

#### 安装jekyll

这步操作起来还是比较蛋疼的,因为rubygems镜像连不上,所以也装不上,需要更换国内的镜像.

国内主流都是使用淘宝的镜像`https://ruby.taobao.org/`,但是我在这里怎么都配置不上去,最终找到了另外一个镜像,山东理工大学的镜像`http://ruby.sdutlinux.org/`,最后成功完成.

{% highlight sh %}
gem sources --remove https://rubygems.org/
gem sources --add http://ruby.sdutlinux.org/
gem install jekyll
{% endhighlight %}

等待过程比较长,耐心等待即可,并没有出问题

### 运行Jekyll

#### 搭建项目框架

建立项目目录, 详细代码参考[我的git项目](https://github.com/bojoyzhou/bojoyzhou.github.io)

{% highlight sh %}
mkdir bojoyzhou.github.io
cd bojoyzhou.github.io
mkdir _layouts
mkdir _posts
touch index.html
{% endhighlight %}

#### 编写第一篇文章

所有的文章都是写在`_posts`目录下面的, 文件名的格式为`年-月-日-文章标题`, 扩展名可以使用`.html`或者`md`

#### 预览

预览命令很简单只有一行,就会自行编译所有文件,在`_site`目录生成相应的静态文件,并且建立一个http服务器,只需要在浏览器访问[http://localhost:4000](http://localhost:4000)即可

{% highlight sh %}
jekyll serve
{% endhighlight %}

### 发布到github

想要部署到github上面,首先需要拥有github帐号,这需要去[github.com](github.com)注册.之后就可以在上面放置自己的项目目录了.

仓库的名字是有讲究的,如果是需要建立个人的默认站点的话,git仓库的名字必须是`username.github.io`

除此之外github还提供给每个项目一个默认站点,这个时候仓库名字就随意了,但是Jekyll的代码必须放置在当前仓库的`ph-pages`分支

[在这里可以找到官方的说明](https://pages.github.com/)

这里建立的是个人站点, 即仓库名字是`username.github.io`

代码同步到github之后就可以通过域名[bojoyzhou.github.io](http://bojoyzhou.github.io)访问了

### 部署到自己的域名

如果自己有域名, 例如[bojoy.name](http://bojoy.name), 此时需要两步即可完成

[这里有官方说明](https://help.github.com/articles/quick-start-setting-up-a-custom-domain/)

1. 添加域名解析服务
    - 在自己的域名解析添加一条A记录,解析到`192.30.252.153`和`192.30.252.154`
2. 告诉github自己的域名是什么
    - 在github仓库的根目录建立一个CNAME文件,里面写一行`bojoy.name`