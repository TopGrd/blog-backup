---
layout: post
category: web
title: node.js连接mysql数据库
tagline: by TopGrd
tags: [nodejs]
---  

---  

<!--more-->  

  今天在学习node时，发现书上的例子是node连接mongodb数据库的，没有提到mysql,而我还没有下载mongodb，就先想连接电脑上已经有点mysql，之前做的东西数据库基本上都用的mysql，经过上网查找相关信息，终于知道如何用node连接mysql进行数据库操作了.  
  首先安装mysql包(nodejs连接mysql的包有好几种(db-mysql..)，这里我用的是mysql。
  
	npm install mysql
    
  然后就是写连接代码了  
     
     /**
     * Created with IntelliJ IDEA.
     * Creator: LeeZhuo
     * Date: 2014/12/3
     * Time: 22:22
     */
    var mysql = require('mysql');
    
    var connection =mysql.createConnection({
        host: 'localhost',  //host
        user: 'topgrd',		//用户名
        password: '',	//密码
        database: 'library'	//要连接的数据库
    });
    /*
    
    var connection = mysql.createConnection('mysql://user:password@host/database');             //另一种写法
    */
    connection.connect();
    /*定义数据库CRUD查询语句*/
    var queryString = 'select * from bookinfo';
    
    connection.query(queryString, function (err, results, field) {
        if(err){
            throw err;
        }
        for(var i in results){
            console.log('bookname: '+results[i].bookname+'\tauthor: '+results[i].author+'\tpressyear: '+results[i].pressyear);
        }
    });
    connection.end();  //关闭连接
    
 上面的代码将我library数据库中bookinfo表的信息打印出来  
 ![photo](/assets/img/mysql.jpg)  
