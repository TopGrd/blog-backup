# 一道题
实现add(x)输出x, add(x)(y)输出x+y的结果，add(x)(y)(z)则输出x+y+z...可以无限调用。  
当我第一眼看到这个题的时候，马上想到的是函数式编程，利用compose实现。要实现这样的函数，必须要改写函数的toString和valueOf方法。
```js
function add() {
  var _args = [].slice.call(arguments);
  var adder = function() {
    var _adder = function() {
      [].push.apply(_args, [].slice.call(arguments));
      console.log('args', _args);
      return _adder;
    }

    _adder.toString = function() {
      return _args.reduce(function(a, b) {
        return a + b;
      });
    }

    return _adder;
  }
  return adder.apply(null, [].slice.call(arguments));
}

console.log(add(2)(3)(3));
```
