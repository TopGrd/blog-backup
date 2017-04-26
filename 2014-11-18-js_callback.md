---  
layout: post  
category: javascript  
title: js回调函数  
tagline: by topgrd  
tags: [javascript]  
---  
javascript callback.  

<!--more-->  

#js回调函数  
*回调函数是把函数当作参数传递给另一个函数，当这个指针被用来调用其所指向的函数时，就称毁掉函数。回调函数不是有该函数的实现方法直接调用，而是在特定的时间或条件发生时由另外的一放调用的，用于对该时间或条件进行响应。*  
举个例子  

	function aa(bb){
    	alert('aa');
        bb();
    }  
    function bb(){
    	alert('bb');
    }
    aa();
    aa(bb);  

运行以上函数，我们发现第一次弹出的是aa，第2次弹出的是aa,bb;  
`aa(bb)`就是用回调函数.  

****  

回调函数是异步编程的最基本方法  
如果有2个函数f1和f2,后者等待前者的执行结果.  
	
    f1();
    f2();  
    
如果f1是一个很耗时的任务,可以把f2写成f1的回调函数.  

	function f1(f2){
    	setTimeout(function(){
        //f1的代码  
        f2();
        },1000)
    }
    
这样执行代码就变成`f1(f2)`  
采用这种方式，将同步操作变为异步操作,f1不会阻塞程序运行,相当于先执行程序的主要逻辑，将耗时的操作推迟执行.  
回调函数的缺点是不利于代码的阅读与维护，各个部分之间高度耦合（Coupling），流程会很混乱，而且每个任务只能指定一个回调函数。