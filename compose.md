# Functional Programing（一）
在数学上，我们定义一个函数y=f(x)或者y=f(g(x))。当我们输入固定的x值时，函数y的值是一定的。而函数式编程即是这么一种风格，它强调副作用最小，鼓励使用不可变数据和纯函数。在如今的js界，函数式编程变的越来越留下。redux，immutable，Rxjs等都是函数式编程的实践。  
## 纯函数  
何谓纯函数？就是同样的输入，结果永远保持不变，非纯函数，则同样的输入会导致不同的结果。 在javascript的原生方法中，数组的splice就是非纯函数，因为它会改变原始数组，并将结果返回。而slice则是纯函数，因为它不会改变原始数组，它返回的是新的数组。纯函数是不会修改变量，它每次返回都是新的变量或者原始变量的拷贝，他不会修改系统变量，没有副作用。  
## 函数柯里化 curry
函数柯里化：只传递给函数一部分参数来调用它，让它返回一个函数去处理剩下的参数。如  
```js
  const f1 = (x, y) => x * y;
  // 柯里化：
  const f2 => x => (y=> x * y);
  // example
  const add = x => (y => x+y);
  const add2 = add(2);
  let result = add2(4); // 6
```  
上面的例子中我们将函数f1柯里化为f2，f2接受第一个参数x会返回一个函数 `x * y`，如add2返回的是2 + y，第二次传入y得到最后结果。  
使用lodash中的curry
```js
  import { curry } from 'lodash';
  const mutiply = curry((x, y) => x * y);
  const mutiply4 = mutiply(4);
  let result = mutiply4(6); // 4 * 6 =24;
```
## 组合 compose  
```js
    const addFour = (x) => x + 4;
    const addSix = (x) => x + 6;
    const compose = (f, g) => ((x) => f(g(x)));
```

addFour函数将参数加4，addSix将参数加6，那么addTen呢，是不是应该addFour后addSix？ 上面的compose函数就是组合函数，将函数f和g组合起来。先执行g(x)，然后将g(x)的结果作为f的参数执行。所以addTen方法如下  
```js
    const addTen => compose(addFour, addSix);
    addTen(1); // 11
```
在 compose 的定义中，g 将先于 f 执行，因此就创建了一个从右到左的数据流。这样做的可读性远远高于嵌套一大堆的函数调用.  
> 让代码从右向左运行，而不是由内而外运行，我觉得可以称之为“左倾”.  

使用compose函数就可以将两个，三个，四个等多个函数黏在一起。
