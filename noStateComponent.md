# React中的组件写法  
## React.createClass  (ES5)  
在React刚出世的时候，官方是这样定义一个react组件的。  
```js
  var Count = React.createClass({
    defaultProps: {
      initialValue: 0
    },
    getInitialState: {
      retrun {
        count: 0
      }
    },
    onChangeHandler: function (e) {
      this.setState({
        count: e.target.value
      })
    },
    render: function() {
      return (
        <div>
          Insert Your Count
          <input
            onChange={this.onChangeHandler} value={this.state.count} />
        </div>
      )
    }
  });
  ReactDOM.render(<Count />, document.getElementById('app'));
```  
## extends React.Component (ES6)  
随着ES6的流行，官方使用了ES6中的Class来创建组件，继承自React.Component，Component是React组件的基类，封装了react组件的属性与方法。在这种写法中，要注意的是this绑定，详情参见我的往期博文。    
```js
  class Count extends React.Component {
    constructor(props) {
      super(props);
      this.state = {
        count: 0
      }
    }

    onChangeHandler(e) {
      this.setState({
        count: e.target.value
      })
    }

    render() {
      return (
        <div>
          Insert Your Count
          <input
            onChange={(e)=>this.onChangeHandler(e)} value={this.state.count} />
        </div>
      )
    }
  }

  Count.defaultProps = {
    initialValue: 0
  }
```  
## 无状态组件 (ES6)
无状态函数式组件，使用纯函数定义的组件，很简洁，但是内部不能使用this，react的state和生命周期方法，所以称为无状态组件。这种组件开销低，在我们写应用时，基本的组件尽量使用它。
```js
  const Header =({ title }) => (
    <h2>{title}</h2>
  )
  
  const Text = ({ name }) => {
    const sayHello = () =>
      alert(`hello ${name}!`);

    return (
      <div>
        Welcome to this room.
        <button onClick={sayHi}>Click It!</button>  
      </div>
    )
  }

```
