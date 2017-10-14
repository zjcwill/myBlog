---
title: 搭建hexo博客踩过的坑
date: 2016-12-15 15:00:00
tags: hexo
---
搭建hexo博客
更换hexo主题
解决百度无法抓取github数据
<!--more-->
初始化hexo博客项目地址 <a href="https://hexo.io/">hexo官网</a>。

```
    npm install hexo-cli -g
    hexo init blog
    cd blog
    npm install
    hexo server
```

## 如何将hexo从本地挂在github并添加cname解析
1.在github新建一个仓库，命名为
`你要设定的名字.github.io`
申请一个密钥,并存入github账户中。
![](http://oi7f2yeu5.bkt.clouddn.com/githubKey.png)

2.在hexo目录下安装git插件
```
$ npm install hexo-deployer-git --save
```
修改配置。
repo填写  `github.com/userName/你要设定的名字.github.io`
```
deploy:
  type: git
  repo: <repository url>
  branch: [branch]
  message: [message]
```
3.在publish文件夹里新建一个叫CNAME的文件，里边要解析的域名。
4.使用`hexo deploy`完成上传
## 更换hexo主题
以NextT 主题为例
首先在<a href="http://theme-next.iissnan.com/getting-started.html#select-scheme">NextT主题官网</a>下载好压缩包，放入theme文件夹并改名为next，在`_config.yml`配置文件中把默认主题修改为next主题`theme: next `,  使用`hexo s --debug`测试主题是否成功启用。
## 解决百度无法抓取github数据
使用国产git工具 <a href="https://coding.net/">coding</a>，绑定github生成`id_rsa.pub`里的密钥文件到coding，建立公共仓库，开启pages服务，里边有选项一个公共仓库可以绑定五个域名。
选择hexo的`_config.yml`,在deploy增加推送分支.
```
deploy:
  type: git
  repo: 
    github: https://github.com/zjcwill/zjcwill.github.io
    coding: https://git.coding.net/zjcwill/zjcwill.git
  brach: master
```
绑定`www`和`@`解析对应不同cname的仓库，即可实现国内百度检索coding仓库下的hexo。
## 主动提交网站sitemap
因为尝试了几次插件无法生成sitemap提交给<a href="http://zhanzhang.baidu.com/">百度站长平台</a>和<a href="https://www.google.com/webmasters/tools/">谷歌Search Console</a>，采取第三方工具，生成后放入`public`中供搜索引擎使用。

