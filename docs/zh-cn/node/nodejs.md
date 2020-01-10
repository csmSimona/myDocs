# nodejs学习笔记

## Node.js是什么

- Node.js不是一门语言，也不是库、框架，它是一个JavaScript运行时环境。
- 简单来讲就是Node.js可以解析和执行JavaScript代码
- 浏览器中的JavaScript
  - EcmaScript
  - BOM
  - DOM
- 构建于Chrome的V8引擎之上
  - 代码只是具有特定格式的字符串而已
  - 引擎可以认识它，可以帮你去解析和执行
  - Node.js的作者把Google Chrome中的V8引擎移植了出来，开发了一个独立的JavaScript运行时环境
- Node.js特性
  - 事件驱动
  - 非阻塞IO模型（异步）
- npm是Node.js开发的
  - npm是世界上最大的开源库生态系统
  - 绝大多数JavaScript相关的包都存放在了npm上，这样做的目的是为了让开发人员更方便的去下载使用

## Node.js 中的 JavaScript

- **没有 BOM、DOM**
- EcmaScript 
- 在 Node 中为 JavaScript 提供了一些服务器级别的 API
  - 文件操作的能力，例如文件读写

    ```JavaScript
    //读取文件.js
    
    // 浏览器中的 JavaScript 是没有文件操作的能力的
    // 但是 Node 中的 JavaScript 具有文件操作的能力
    
    // fs 是 file-system 的简写，就是文件系统的意思
    // 在 Node 中如果想要进行文件操作，就必须引入 fs 这个核心模块
    // 在 fs 这个核心模块中，就提供了所有的文件操作相关的 API
    // 例如：fs.readFile 就是用来读取文件的
    
    // 1. 使用 require 方法加载 fs 核心模块
    var fs = require('fs')
    
    // 2. 读取文件
    //    第一个参数就是要读取的文件路径
    //    第二个参数是一个回调函数
    //          
    //        成功
    //          data 数据
    //          error null
    //        失败
    //          data undefined没有数据
    //          error 错误对象
    fs.readFile('./data/hello.txt', function (error, data) {
      // <Buffer 68 65 6c 6c 6f 20 6e 6f 64 65 6a 73 0d 0a>
      // 文件中存储的其实都是二进制数据 0 1
      // 这里为什么看到的不是 0 和 1 呢？原因是二进制转为 16 进制了
      // 但是无论是二进制01还是16进制，人类都不认识
      // 所以我们可以通过 toString 方法把其转为我们能认识的字符
      // console.log(data)
    
      // console.log(error)
      // console.log(data)
    
      // 在这里就可以通过判断 error 来确认是否有错误发生
      if (error) {
        console.log('读取文件失败了')
      } else {
        console.log(data.toString())
      }
    })
    
    ```

    ```JavaScript
    //写文件.js
    var fs = require('fs')
    
    // $.ajax({
    //   ...
    //   success: function (data) {
        
    //   }
    // })
    
    // 第一个参数：文件路径
    // 第二个参数：文件内容
    // 第三个参数：回调函数
    //    error
    //    
    //    成功：
    //      文件写入成功
    //      error 是 null
    //    失败：
    //      文件写入失败
    //      error 就是错误对象
    fs.writeFile('./data/你好.md', '大家好，给大家介绍一下，我是Node.js', function (error) {
      // console.log('文件写入成功')
      // console.log(error)
      if (error) {
        console.log('写入失败')
      } else {
        console.log('写入成功了')
      }
    })
    
    ```

  - 网络服务的构建

  - 网络通信

  - http服务器

    ```JavaScript
    // 可以使用 Node 非常轻松的构建一个 Web 服务器
    // 在 Node 中专门提供了一个核心模块：http
    // http 这个模块的职责就是帮你创建编写服务器的
    
    // 1. 加载 http 核心模块
    var http = require('http')
    
    // 2. 使用 http.createServer() 方法创建一个 Web 服务器
    //    返回一个 Server 实例
    var server = http.createServer()
    
    // 3. 服务器要干嘛？
    //    提供服务：对数据的服务
    //    发送请求
    //    接收请求
    //    处理请求
    //    给个反馈（发送响应）
    //    注册 request 请求事件
    //    当客户端请求过来，就会自动触发服务器的 request 请求事件，然后执行第二个参数：回调处理函数
    server.on('request', function () {
      console.log('收到客户端的请求了')
    })
    
    // 4. 绑定端口号，启动服务器
    server.listen(3000, function () {
      console.log('服务器启动成功了，可以通过 http://127.0.0.1:3000/ 来进行访问')
    })
    
    ```

    ```javascript
    //http-res.js
    var http = require('http')
    
    var server = http.createServer()
    
    // request 请求事件处理函数，需要接收两个参数：
    //    Request 请求对象
    //        请求对象可以用来获取客户端的一些请求信息，例如请求路径
    //    Response 响应对象
    //        响应对象可以用来给客户端发送响应消息
    server.on('request', function (request, response) {
      // http://127.0.0.1:3000/ /
      // http://127.0.0.1:3000/a /a
      // http://127.0.0.1:3000/foo/b /foo/b
      console.log('收到客户端的请求了，请求路径是：' + request.url)
    
      // response 对象有一个方法：write 可以用来给客户端发送响应数据
      // write 可以使用多次，但是最后一定要使用 end 来结束响应，否则客户端会一直等待
      response.write('hello')
      response.write(' nodejs')
    
      // 告诉客户端，我的话说完了，你可以呈递给用户了
      response.end()
    
      // 由于现在我们的服务器的能力还非常的弱，无论是什么请求，都只能响应 hello nodejs
      // 思考：
      //  我希望当请求不同的路径的时候响应不同的结果
      //  例如：
      //  / index
      //  /login 登陆
      //  /register 注册
      //  /haha 哈哈哈
    })
    
    server.listen(3000, function () {
      console.log('服务器启动成功了，可以通过 http://127.0.0.1:3000/ 来进行访问')
    })
    
    ```

    ```javascript
    //http-url-res.js
    var http = require('http')
    
    // 1. 创建 Server
    var server = http.createServer()
    
    // 2. 监听 request 请求事件，设置请求处理函数
    server.on('request', function (req, res) {
      console.log('收到请求了，请求路径是：' + req.url)
      console.log('请求我的客户端的地址是：', req.socket.remoteAddress, req.socket.remotePort)
    
      // res.write('hello')
      // res.write(' world')
      // res.end()
    
      // 上面的方式比较麻烦，推荐使用更简单的方式，直接 end 的同时发送响应数据
      // res.end('hello nodejs')
    
      // 根据不同的请求路径发送不同的响应结果
      // 1. 获取请求路径
      //    req.url 获取到的是端口号之后的那一部分路径
      //    也就是说所有的 url 都是以 / 开头的
      // 2. 判断路径处理响应
    
      var url = req.url
    
      if (url === '/') {
        res.end('index page')
      } else if (url === '/login') {
        res.end('login page')
      } else if (url === '/products') {
        var products = [{
            name: '苹果 X',
            price: 8888
          },
          {
            name: '菠萝 X',
            price: 5000
          },
          {
            name: '小辣椒 X',
            price: 1999
          }
        ]
    
        // 响应内容只能是二进制数据或者字符串
        //  数字
        //  对象
        //  数组
        //  布尔值
        res.end(JSON.stringify(products))
      } else {
        res.end('404 Not Found.')
      }
    })
    
    // 3. 绑定端口号，启动服务
    server.listen(3000, function () {
      console.log('服务器启动成功，可以访问了。。。')
    })
    
    ```


## 模块系统

- 在 Node 中没有全局作用域的概念
- 在 Node 中，只能通过 require 方法来加载执行多个 JavaScript 脚本文件
- require 加载只能是执行其中的代码，文件与文件之间由于是模块作用域，所以不会有污染的问题
  - 模块完全是封闭的
  - 外部无法访问内部
  - 内部也无法访问外部
- 模块作用域固然带来了一些好处，可以加载执行多个文件，可以完全避免变量命名冲突污染的问题
- 但是某些情况下，模块与模块是需要进行通信的
- 在每个模块中，都提供了一个对象：`exports`
- 该对象默认是一个空对象
- 你要做的就是把需要被外部访问使用的成员手动的挂载到 `exports` 接口对象中
- 然后谁来 `require` 这个模块，谁就可以得到模块内部的 `exports` 接口对象

## 核心模块

- 核心模块是由 Node 提供的一个个的具名的模块，它们都有自己特殊的名称标识，例如
  - fs 文件操作模块

  - http 网络服务构建模块

  - os 操作系统信息模块

  - path 路径处理模块

    ```javascript
    // 用来获取机器信息的
    var os = require('os')
    
    // 用来操作路径的
    var path = require('path')
    
    // 获取当前机器的 CPU 信息
    console.log(os.cpus())
    
    // memory 内存
    console.log(os.totalmem())
    
    // 获取一个路径中的扩展名部分
    // extname extension name
    console.log(path.extname('c:/a/b/c/d/hello.txt'))
    ```

- 所有核心模块在使用的时候都必须手动的先使用 `require` 方法来加载，然后才可以使用，例如：

  - `var fs = require('fs')`          (require是同步的)

    ```javascript
    //加载
    
    //a.js
    // require 是一个方法
    // 它的作用就是用来加载模块的
    // 在 Node 中，模块有三种：
    //    具名的核心模块，例如 fs、http
    //    用户自己编写的文件模块
    //      相对路径必须加 ./
    //      可以省略后缀名
    //      相对路径中的 ./ 不能省略，否则报错
    //    在 Node 中，没有全局作用域，只有模块作用域
    //      外部访问不到内部
    //      内部也访问不到外部
    //      默认都是封闭的
    //    既然是模块作用域，那如何让模块与模块之间进行通信
    //    有时候，我们加载文件模块的目的不是为了简简单单的执行里面的代码，更重要是为了使用里面的某个成员
    
    var foo = 'aaa'
    
    console.log('a start')
    
    function add(x, y) {
      return x + y
    }
    
    // Error: Cannot find module 'b'
    // require('b')
    
    // 可以
    // require('./b.js')
    
    // 推荐：可以省略后缀名
    require('./b')
    
    console.log('a end')
    
    console.log('foo 的值是：', foo)
    
    
    //b.js
    console.log('b start')
    
    // console.log(add(10, 20))
    
    var foo = 'bbb'
    
    require('./c.js')
    console.log('b end')
    
    
    //c.js
    console.log('b start')
    
    // console.log(add(10, 20))
    
    var foo = 'bbb'
    
    require('./c.js')
    console.log('b end')
    
    ```

    ```javascript
    //导出
    
    //a.js
    // require 方法有两个作用：
    //    1. 加载文件模块并执行里面的代码
    //    2. 拿到被加载文件模块导出的接口对象
    //    
    //    在每个文件模块中都提供了一个对象：exports
    //    exports 默认是一个空对象
    //    你要做的就是把所有需要被外部访问的成员挂载到这个 exports 对象中
    var bExports = require('./b')
    var fs = require('fs')
    
    console.log(bExports.foo)
    
    console.log(bExports.add(10, 30))
    
    console.log(bExports.age)
    
    bExports.readFile('./a.js')
    
    fs.readFile('./a.js', function (err, data) {
      if (err) {
        console.log('读取文件失败')
      } else {
        console.log(data.toString())
      }
    })
    
    
    //b.js
    var foo = 'bbb'
    
    // console.log(exports)
    
    exports.foo = 'hello'
    
    exports.add = function (x, y) {
      return x + y
    }
    
    exports.readFile = function (path, callback) {
      console.log('文件路径：', path)
    }
    
    var age = 18
    
    exports.age = age
    
    function add(x, y) {
      return x - y
    }
    
    ```

    

## web服务器开发

- require
- 端口号
  - ip 地址定位计算机

  - 端口号定位具体的应用程序

  - 一切需要联网通信的软件都会占用一个端口号

  - 端口号的范围从0-65536之间

  - 在计算机中有一些默认端口号，最好不要去使用，例如http服务的80

  - 我们在开发过程中使用一些简单好记的就可以了，例如3000、5000等没什么含义的

    ```javascript
    // ip 地址用来定位计算机
    // 端口号用来定位具体的应用程序
    // 所有需要联网通信的应用程序都会占用一个端口号
    
    var http = require('http')
    
    var server = http.createServer()
    
    // 2. 监听 request 请求事件，设置请求处理函数
    server.on('request', function (req, res) {
      console.log('收到请求了，请求路径是：' + req.url)
      console.log('请求我的客户端的地址是：', req.socket.remoteAddress, req.socket.remotePort)
    
      res.end('hello nodejs')
    })
    
    server.listen(5000, function () {
      console.log('服务器启动成功，可以访问了。。。')
    })
    
    ```

- Content-Type
  - 服务器最好把每次响应的数据是什么内容类型都告诉客户端，而且要正确的告诉

  - 不同的资源对应的 Content-Type 是不一样，具体参照：http://tool.oschina.net/commons

  - 对于文本类型的数据，最好都加上编码，目的是为了防止中文解析乱码问题

    ```javascript
    // require
    // 端口号
    
    var http = require('http')
    
    var server = http.createServer()
    
    server.on('request', function (req, res) {
      // 在服务端默认发送的数据，其实是 utf8 编码的内容
      // 但是浏览器不知道你是 utf8 编码的内容
      // 浏览器在不知道服务器响应内容的编码的情况下会按照当前操作系统的默认编码去解析
      // 中文操作系统默认是 gbk
      // 解决方法就是正确的告诉浏览器我给你发送的内容是什么编码的
      // 在 http 协议中，Content-Type 就是用来告知对方我给你发送的数据内容是什么类型
      // res.setHeader('Content-Type', 'text/plain; charset=utf-8')
      // res.end('hello 世界')
    
      var url = req.url
    
      if (url === '/plain') {
        // text/plain 就是普通文本
        res.setHeader('Content-Type', 'text/plain; charset=utf-8')
        res.end('hello 世界')
      } else if (url === '/html') {
        // 如果你发送的是 html 格式的字符串，则也要告诉浏览器我给你发送是 text/html 格式的内容
        res.setHeader('Content-Type', 'text/html; charset=utf-8')
        res.end('<p>hello html <a href="">点我</a></p>')
      }
    })
    
    server.listen(3000, function () {
      console.log('Server is running...')
    })
    
    ```

- 通过网络发送文件
  - 发送的并不是文件，本质上来讲发送是文件的内容

  - 当浏览器收到服务器响应内容之后，就会根据你的 Content-Type 进行对应的解析处理

    ```javascript
    // 1. 结合 fs 发送文件中的数据
    // 2. Content-Type
    //    http://tool.oschina.net/commons
    //    不同的资源对应的 Content-Type 是不一样的
    //    图片不需要指定编码
    //    一般只为字符数据才指定编码
    
    var http = require('http')
    var fs = require('fs')
    
    var server = http.createServer()
    
    server.on('request', function (req, res) {
      // / index.html
      var url = req.url
    
      if (url === '/') {
        // 肯定不这么干
        // res.end('<!DOCTYPE html><html lang="en"><head><meta charset="UTF-8"><title>Document</title></head><body><h1>首页</h1></body>/html>')
    
        // 我们要发送的还是在文件中的内容
        fs.readFile('./resource/index.html', function (err, data) {
          if (err) {
            res.setHeader('Content-Type', 'text/plain; charset=utf-8')
            res.end('文件读取失败，请稍后重试！')
          } else {
            // data 默认是二进制数据，可以通过 .toString 转为咱们能识别的字符串
            // res.end() 支持两种数据类型，一种是二进制，一种是字符串
            res.setHeader('Content-Type', 'text/html; charset=utf-8')
            res.end(data)
          }
        })
      } else if (url === '/xiaoming') {
        // url：统一资源定位符
        // 一个 url 最终其实是要对应到一个资源的
        fs.readFile('./resource/ab2.jpg', function (err, data) {
          if (err) {
            res.setHeader('Content-Type', 'text/plain; charset=utf-8')
            res.end('文件读取失败，请稍后重试！')
          } else {
            // data 默认是二进制数据，可以通过 .toString 转为咱们能识别的字符串
            // res.end() 支持两种数据类型，一种是二进制，一种是字符串
            // 图片就不需要指定编码了，因为我们常说的编码一般指的是：字符编码
            res.setHeader('Content-Type', 'image/jpeg')
            res.end(data)
          }
        })
      }
    })
    
    server.listen(3000, function () {
      console.log('Server is running...')
    })
    
    ```

## 代码风格

- [JavaScript Standard Style](https://standardjs.com/)

- Airbnb JavaScript Style

- 当一行代码是以：( 、[、`（反引号），开头的时候，则在前面补上一个分号用以避免一些语法解析错误。

  所以你会发现在一些第三方的代码中能看到一上来就以一个 ; 开头。

## 在node中使用模板引擎

在 Node 中使用 art-template 模板引擎

模板引起最早就是诞生于服务器领域，后来才发展到了前端。

1. 安装 npm install art-template

2. 在需要使用的文件模块中加载 art-template

3. 查文档，使用模板引擎的 API

```html
<!-- tpl.html -->

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>{{ title }}</title>
</head>
<body>
  <p>大家好，我叫：{{ name }}</p>
  <p>我今年 {{ age }} 岁了</p>
  <h1>我来自 {{ province }}</h1>
  <p>我喜欢：{{each hobbies}} {{ $value }} {{/each}}</p>
  <script>
    var foo = '{{ title }}'
  </script>
</body>
</html>
```

```js
var template = require('art-template')
var fs = require('fs')

fs.readFile('./tpl.html', function (err, data) {
  if (err) {
    return console.log('读取文件失败了')
  }
  // 默认读取到的 data 是二进制数据
  // 而模板引擎的 render 方法需要接收的是字符串
  // 所以我们在这里需要把 data 二进制数据转为 字符串 才可以给模板引擎使用
  var ret = template.render(data.toString(), {
    name: 'Jack',
    age: 18,
    province: '北京市',
    hobbies: [
      '写代码',
      '唱歌',
      '打游戏'
    ],
    title: '个人信息'
  })

  console.log(ret)
})
```



## 客户端渲染和服务端渲染

有两张图

- 客户端渲染

  1.第一次请求拿到的是页面

  2.第二次请求拿到的是数据

  浏览器渲染过程： 

  ​	1.收到服务端响应的字符串了

  ​	2.从上到下一次解析，在解析的过程中，如果发现ajax请求，则再次发起新的请求

  ​	3.发请求

  ​	4.拿到ajax响应结果

  ​	5.模板引擎渲染

- 服务端渲染

  - 在服务端使用模板引擎

  - 模板引擎最早诞生于服务端，后来才发展到了前端

  - 对于服务端渲染来说，只请求了一次。服务端渲染，响应的就是最终的结果。客户端不需要再做任何处理

  - 服务器渲染过程：

    1.读取index.html

    2.模板引起渲染，在发送给客户端之前，我在服务端就已经把index.html渲染处理了

- 服务端渲染和客户端渲染的区别

  - 客户端渲染不利于 SEO 搜索引擎优化
  - 服务端渲染是可以被爬虫抓取到的，客户端异步渲染是很难被爬虫抓取到的
  - 所以你会发现真正的网站既不是纯异步也不是纯服务端渲染出来的
  - 而是两者结合来做的
  - 例如京东的商品列表就采用的是服务端渲染，目的了为了 SEO 搜索引擎优化
  - 而它的商品评论列表为了用户体验，而且也不需要 SEO 优化，所以采用是客户端渲染

- 如何通过服务器让客户端重定向？

  1.状态码设置为 302 临时重定向`statusCode`

  2.在响应头中通过 Location 告诉客户端往哪儿重定向`setHeader`

  ​	如果客户端发现收到服务器的响应的状态码是 302 就会自动去响应头中找 Location ，然后对该地址发起新的请求

  ```js
  res.statusCode = 302
  res.setHeader('Location', 要跳转的路径)
  ```

## exports 和 module.exports 的区别

- 每个模块中都有一个 module 对象，module 对象中有一个 exports 对象
- 我们可以把需要导出的成员都挂载到 module.exports 接口对象中，也就是：`moudle.exports.xxx = xxx` 的方式
- 但是每次都 `moudle.exports.xxx = xxx` 很麻烦，点儿的太多了
- 所以 Node 为了你方便，同时在每一个模块中都提供了一个成员叫：`exports`
- `exports === module.exports` 结果为  `true`s
- 所以对于：`moudle.exports.xxx = xxx` 的方式 完全可以：`expots.xxx = xxx`
- 当一个模块需要导出单个成员的时候，这个时候必须使用：`module.exports = xxx` 的方式
- 不要使用 `exports = xxx` 不管用
- 因为每个模块最终向外 `return` 的是 `module.exports`
- 而 `exports` 只是 `module.exports` 的一个引用
- 所以即便你为 `exports = xx` 重新赋值，也不会影响 `module.exports`
- 但是有一种赋值方式比较特殊：`exports = module.exports` 这个用来重新建立引用关系的

```javascript
moudle.exports = {
  a: 123
}

// 重新建立 exports 和 module.exports 之间的引用关系
exports = module.exports

exports.foo = 'bar'
```

## require 方法加载规则（模块查找机制）

- 优先从缓存加载
- 核心模块
- 路径形式的模块
- 第三方模块

  - 凡是第三方模块都必须通过 npm 来下载，通过 require('包名') 的方式来进行加载才可以使用

  - 不可能有任何一个第三方包和核心模块的名字是一样的

  - - ​     node_modules/art-template/

    - ​     node_modules/art-template/package.json

    - ​     node_modules/art-template/package.json main

    - ​    如果 package.json 文件不存在或者 main 指定的入口模块是也没有，则 node 会自动找该目录下的 index.js，也就是说 index.js 会作为一个默认备选项；

    - ​     进入上一级目录找 node_modules

    - ​     按照这个规则依次往上找，直到磁盘根目录还找不到，最后报错：Can not find moudle xxx

  - 一个项目有且仅有一个 node_modules 而且是存放到项目的根目录

    
