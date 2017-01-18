#浏览器兼容  
* ie9不支持placeholder
* IE8不支持 __proto__
* IE9不支持监听输入框退格事件
* window.onload存在兼容性问题
* decodeURIComponent()存在Uncaught URIError: URI malformed问题，如decodeURIComponent('a%AFc')。  
# notice  
* addEventListener的handler使用bind的时候， 需要保存bind后的handler，才能remove。  
```js  
  var touchHandler = function (e) {
    // do something
  }
  var hanlder = touchHandler.bind(this);
  document.addEventListener('touchstart', handler, false);
  // when remove
  document.removeEventListener('touchstart', handler, false);
  
```  
