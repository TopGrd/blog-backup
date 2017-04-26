# React + ES6 中绑定this  
在使用React.creatClass时，如果给一个组件绑定事件（onClick，onChange等），是不需要将this在bind到上面的，然而在使用ES6时，是不会自动绑定this的。why？  
Go Doc:  
> **Autobinding**  
When creating callbacks in JavaScript, you usually need to explicitly bind a method to its instance such that the value of this is correct. With React, every method is automatically bound to its component instance (except when using ES6 class syntax). React caches the bound method such that it's extremely CPU and memory efficient. It's also less typing!  

在React中，如果创建了回调函数，是会自动将this绑定到他的组件上面的。**(except when using Es6 class syntax)** , :(  
> **No Autobinding**  
Methods follow the same semantics as regular ES6 classes, meaning that they don't automatically bind this to the instance. You'll have to explicitly use .bind(this) or arrow functions =>:  

所以在使用ES6写react组件时，可以这么写：  
**第一种**  
```js
_handleClick(e) {
    console.log(this);
}
render() {
    return (
        <div>
            <h1 onClick={this._handleClick.bind(this)}>点击</h1>
        </div>
    );
}
```  
**第二种**  
```js
_handleClick(e) {
    console.log(this);
}
render() {
    return (
        <div>
            <h1 onClick={()=>this._handleClick()}>点击</h1>
        </div>
    );
}
```
**第三种**  
```js
constructor() {
    this._handlerClick = this._handlerClick.bind(this);
}
_handleClick(e) {
    console.log(this);
}
render() {
    return (
        <div>
            <h1 onClick={this._handleClick}>点击</h1>
        </div>
    );
}
```
**第四种**  
```js
_handleClick(e) {
    console.log(this);
}
render() {
    return (
        <div>
            <h1 onClick={::this._handleClick}>点击</h1>
        </div>
    );
}
```
特别解释下第四种  
函数绑定运算符是并排的两个双冒号（::），双冒号左边是一个对象，右边是一个函数。该运算符会自动将左边的对象，作为上下文环境（即this对象），绑定到右边的函数上面，ES7的草案，babel已经支持。  
facebook关于没有自动绑定的介绍:[autobind](https://facebook.github.io/react/docs/reusable-components.html#no-autobinding)
