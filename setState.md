# React中的setState是异步的。
在写Select组件时，发现我换了选项后，结果依然返回之前的值，导致我的选项与值的展示不对应。以下是关于这个问题的解释：  
先看源码ReactComponent.js中关于setState函数的文档  
> 绝对不要直接改变 this.state，因为在之后调用 setState() 可能会替换掉你做的更改。把 this.state 当做不可变的。  
setState() 不会立刻改变 this.state，而是创建一个即将处理的 state 转变。在调用该方法之后获取 this.state 的值可能会得到现有的值，而不是最新设置的值。  
不保证 setState() 调用的同步性，为了提升性能，可能会批量执行 state 转变和 DOM 渲染。  
setState() 将总是触发一次重绘，除非在 shouldComponentUpdate() 中实现了条件渲染逻辑。如果使用可变的对象，但是又不能在   shouldComponentUpdate() 中实现这种逻辑，仅在新 state 和之前的 state 存在差异的时候调用 setState() 可以避免不必要的重新渲染。  

```javascript

/**
* Sets a subset of the state. Always use this to mutate
* state. You should treat `this.state` as immutable.
*
* There is no guarantee that `this.state` will be immediately updated, so
* accessing `this.state` after calling this method may return the old value.
*
* There is no guarantee that calls to `setState` will run synchronously,
* as they may eventually be batched together.  You can provide an optional
* callback that will be executed when the call to setState is actually
* completed.
*
* When a function is provided to setState, it will be called at some point in
* the future (not synchronously). It will be called with the up to date
* component arguments (state, props, context). These values can be different
* from this.* because your function may be called after receiveProps but before
* shouldComponentUpdate, and this new state, props, and context will not yet be
* assigned to this.
*
* @param {object|function} partialState Next partial state or function to
*        produce next partial state to be merged with current state.
* @param {?function} callback Called after state is updated.
* @final
* @protected
*/
ReactComponent.prototype.setState = function (partialState, callback) {
    !(typeof partialState === 'object' || typeof partialState === 'function' || partialState == null)
        ? true
            ? invariant(false, 'setState(...): takes an object of state variables to update or a function which returns an object of state variables.')
            : _prodInvariant('85')
        : void 0;
    this.updater.enqueueSetState(this, partialState);
    if (callback) {
        this.updater.enqueueCallback(this, callback, 'setState');
    }
};
```  
文档解释了setState()是异步执行的，所以在setState中提供了回调函数，所以可以把setState后面的动作设置到回调函数里，:)
