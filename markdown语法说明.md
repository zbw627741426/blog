---
title: Markdown语法说明
date: 2017/06/22 21:37:00
---
## Markdown简单介绍
> HTML is a _publishing_ format;Markdown is a _writing_ format.  
Markdown is intended to be as easy-to-read and easy-to-write as is feasible.

[Markdown官网](http://daringfireball.net/projects/Markdown)

## 段落
段落之间至少以**一个空行隔开**，通常来说段落的**首字符不需要缩进**。  
换行的方式是：末尾至少**两个空格然后回车**。

## 标题
标题有两种形式：
### 1. Setext
  - 一级标题（标题下一行输入“=”等于号）

    ====
  - 二级标题（标题下一行输入“-”减号）  

    \-\-\-\-  

### 2. atx  
  输入1～6个#来定义1～6级标题

## 引用
使用">"引用，配合这上述换行方法会让引用更美观。  
一种方法是**每一行**前面都加上">"符号；  
另一种方法是**段落首字符**前加上">"符号。
">"引用符号后面可以继续接其他修饰符号，如"##" 、"1. "等。  

## 列表
### 1. 有序列表  
数字的顺序并不影响转换从HTML后列表顺序。  
可以使用转义字符"\\"来避免列表标志与类似“2017\\.12.24”形式开头的冲突。
### 2. 无序列表  
"+" "-" "\*" 都可以作为无序列表符号。  
列表中每一条项目可以包含**多个段落**，这时从第二个段落开始，首字符必须与第一行首字符对齐。  
列表条目中有">"，需要缩进4格；列表中有代码块，需要缩进8格。  

## 代码块  
    行首缩进至少4格

## 水平线
    ---
    ***
    *****
    * * * *
    -------------------------

都可以画出一条水平线。  

## 连接  
两种形式，一种是外部链接，一种是页内链接：  
### 1. 链接文字与链接地址写在一起  
  \[text\](URL) URL既可以是网址，也可以是URI。
### 2. 链接文字与链接地址分开写  
  页面内某处写\[text][id]  
  页面另外某处，一般在最后写[id]: http://example.com  
  id可以是数字、也可以是字母或者带空格甚至不写，如果不写的话，id就是前面的text文字。  

        [text][id]
        [id]: http://www.example.com
        [text][]
        [text]: http://www.example.com

## 强调
        *italic*
        _italic_
        **strong**
        __strong__

## 代码  
`` `pringf()` `` `pringf()`  

## 图片  
同链接一样都有两种形式：
1.

        ！[image text](URL)
2.

        ![image text][id]
        [id]: URL

## 显示链接  
        <http://www.example.com>
        <example@abc.com>

## 转义字符
`\` 可以转义的符号有：

        \ backslash
        ` backtick
        * asterisk
        _ underscore
        {} curly braces
        [] square brackets
        () parentheses
        # hash mark
        + plus sign
        - minus sign
        . dot
        ! exclamation mark
