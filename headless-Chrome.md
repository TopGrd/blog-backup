# Windows下使用Headless Chrome  
google在4月的时候宣布他们将在chrome 59中支持headless模式，headless模式即chromr会以一种静默的模式激动，他不会启用界面，但是他在后台的行为与正常浏览器一样。  
## 准备  
安装一个支持headless的chrome版本，我使用的是chrome canary，是chrome的实验版本，新的特性一版都会最新添加在里面。  
## 启动  
最简单的启动方式是在桌面上右键chrome，然后在目标后面添加`--headless --remote-debugging-port=9222 --disable-gpu https://chromium.org`,然后右键，这样chrome就在后台以headless模式运行了，并且监听的9222端口。或者使用命令行的方式打开 在后面添加刚才的参数  
## 使用chrome-remote-interface
使用npm的包[chrome-remote-interface](https://github.com/cyrus-and/chrome-remote-interface)会让我们更方便的完成想要的操作，它允许使用配置远程链接chrome，然后调用api（chrome debugger-protocol）去操作。  
## 代码  
以下代码完成了3个操作，分别调用了Network Page Console，主要的功能是监听console.messageAdded事件，一旦console有消音添加，会在cmd/bash中打印
，打印网络请求，打印页面img的属性。
```js
const CDP = require("chrome-remote-interface")

CDP(chrome => {
  const { Network, Page, Console } = chrome

  Network.requestWillBeSent(params => {
    console.log(params.request.url)
  })

  chrome.on("Console.messageAdded", function(message) {
    console.log(message.message.text)
  })

  Promise.all([Network.enable(), Page.enable(), Console.enable()])
    .then(() => {
      return Page.navigate({
        url: "http://topgrd.me"
      })
    })
    .then(() => {
      setTimeout(function() {
        chrome.DOM.getDocument((error, params) => {
          if (error) {
            console.error(params)
            return
          }
          const options = {
            nodeId: params.root.nodeId,
            selector: "img"
          }
          chrome.DOM.querySelectorAll(options, (error, params) => {
            if (error) {
              console.error(params)
              return
            }
            console.log(params)
            params.nodeIds.forEach(nodeId => {
              const options = {
                nodeId: nodeId
              }
              chrome.DOM.getAttributes(options, (error, params) => {
                if (error) {
                  console.error(params)
                  return
                }
              })
            })
          })
        })
      }, 5000)
    })
    .catch(err => {
      console.error(err)
      chrome.close()
    })
}).on("error", err => {
  console.error(err)
})

```

## 可以做什么
chrome的headless模式可以让我们完成爬虫，自动化测试等相关功能。