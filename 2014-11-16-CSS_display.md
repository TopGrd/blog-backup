---
layout: post
category: web
title: 前端小知识
tagline: by topgrd  
tags: [FE, css]
---
前端的小知识，看看你知道不知道.

<!--more-->

# 前端知识

#css hack#

IE6 hack

    _background-color:#CDCDCD;

IE7 hack

　　*background-color:#dddd00;
  
IE8 hack

　　background-color:red \0;
  
IE9 hack

    background-color:blue \9\0; 
    

#浏览器是如何判断元素是否匹配某个 CSS 选择器？#

比如#divBox p span.red{color:red;}，浏览器的查找顺序如下：

 1. 先查找html中所有class='red'的span元素
 2. 再查找其父辈元素中是否有p元素
 3. 判断p的父元素中是否有id为divBox的div元素，如果都存在则匹配上。

        <style>
        DIV#divBox p span.red{color:red;}
        </style>
        <body>
        <div id="divBox">
        <p><span>s1</span></p>
        <p><span>s2</span></p>
        <p><span>s3</span></p>
        <p><span class='red'>s4</span></p>
        </div>
        </body>
