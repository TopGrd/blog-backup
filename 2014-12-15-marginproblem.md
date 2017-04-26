---
layout: post
category: web
title: margin相关问题
tagline: by TopGrd
tags: [css]
---  

---  

<!--more-->  

##上下margin叠加  
  当两个元素为上下关系，且都具有margin属性时，此时margin会造成外边距叠加。  
  例如，页面有2个div id为a和b，他们的css如下:  
    
    #a{
    	width:100px;
		height:100px;
		background:red;
		margin:10px;
    }  
    #b{
    	width:100px;
		height:100px;
		background:red;
		margin:10px;
    }  
    
  这两个元素都有上下边距为10px，按道理说他们两之间应该上下相隔20px。但浏览器显示结果并非这样。从下图通过左右的间距对比可以看出他们之间只相隔10px。  
  ![margin1](/assets/img/margin1.jpg)   
  为什么会这样呢，通过网上搜寻以后发现这是css设计造成的。因为他们考虑到如果我们要对段落进行控制，如果第一段与上方距离10px，那第二段与第一段之间的距离就变成20px，这不是我们想要的，因此设计出了空白边叠加规则。  
  空白边叠加时，以较大的margin值为准。  
  怎么解决这个问题呢，根据css解释规则，在把元素设置float后，将不再进行margin叠加  
  
    #a{
    	width:100px;
		height:100px;
		background:red;
		margin:10px;
        float:left;
    }  
    #b{
    	width:100px;
		height:100px;
		background:red;
		margin:10px;
        float:left;
        clear:left;
    }  
    
 结果得到如下图的效果   
 ![margin2](/assets/img/margin2.jpg)    
 我们看到a和b之间的间隔已经变为20px。   
 ##IE6下元素float后margin左右边距加倍  
 在IE6下如果元素设置浮动后，元素的左右边距会加倍。也就是常听到的IE6双边距问题。但我们只需要在元素的样式中添加`display:inline`就可以解决。  
 
