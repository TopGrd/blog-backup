# Functional Programing (二)  
## Functor
### Container  
创建一个容器Container,里面可以存储任意值  
```js
function Container(x) {
  this.__value = x
}
```

但是我们如果创建一个容器，每次都需要写new，可以创建一个of函数来避免。  
```js
Container.of = function (x) {
  return new Container(x)
}
```

这样，如果构造一个新的容器，则只需要`Container.of(x)`就行了。 如果容器中有了值，我们需要一个方法能够操作这个值。
```js
Container.prototype.map = function (f) {
  return Container.of(f(this.__value))
}
```

利用map方法，将想要操作这个值的方法传递进去，操作容器内的值，并返回一个新的容器和操作后的值。