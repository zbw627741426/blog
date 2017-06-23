title: HEXO博客框架说明  
date: 2017/06/23
---

## 1. HEXO介绍
> HEXO is a fast, simple and powerful blog framework. You write posts in Markdown (or other languages) and HEXO generates static files with a beautiful theme in seconds.

[HEXO](https://HEXO.io/)可以使你只需要关注文章内容，而其余格式、发布、主题等都可以自动化完成。

## 2. HEXO在CentOS7下的安装方法
需要安装的软件有：  
- nodejs
- git
- HEXO

        yum -y install epel-release nodejs git

[nodejs](https://nodejs.org/en/)安装完成后使用npm安装。
> NPM是随同NodeJS一起安装的包管理工具，能解决NodeJS代码部署上的很多问题，常见的使用场景有以下几种：  
1. 允许用户从NPM服务器下载别人编写的第三方包到本地使用。
2. 允许用户从NPM服务器下载并安装别人编写的命令行程序到本地使用。
3. 允许用户将自己编写的包或命令行程序上传到NPM服务器供别人使用。

        npm -g install hexo-cli

下一步就是安装HEXO

        $ hexo init <folder>
        $ cd <folder>
        $ npm install

## 3. 配置HEXO
修改_config.yml文件，  
HEXO官网文档讲的很详细，具体可以参考[这里](https://HEXO.io/zh-cn/docs/configuration.html)。
我修改的有这么几处：

        title 	      网站标题
        subtitle 	    网站副标题
        description 	网站描述
        author 	      您的名字
        language 	    网站使用的语言
        url 	        网址 	
        root 	        网站根目录
        public_dir 	  公共文件夹，这个文件夹用于存放生成的站点文件
        theme 	      当前主题名称，值为false时禁用主题

## 4. 如何写博客并发布  
`hexo new [layout] <title>`  新建文章`title`中有空格需要用双引号
`hexo generate`  发布`source/_post/`中的文章  
`hexo publish`  发布`source/_draft/`中的草稿  
`hexo deploy`  部署到远程服务器上，使用前需要在_config.yml中配置git或者FTP。  
图片等资源可以存在`source`文件夹中。

## 5. 更换主题theme  
Find and download a theme from [here](https://HEXO.io/themes/).  
Use `git clone `to the /themes/.  
Configure \_config.yml , change the attribution of themes to your theme.  
And according to yourself ,you may need to configure the  `themes/yourtheme/\_config.yml`.Especially you had changed the root url.  
