# React16+Redux 实战企业级大众点评Web App

- 初始化项目

```shell
npx create-react-app helloworld

cd helloworld

npm start
```

- 使用mock数据

方式一：代理到mock服务器

mock文件： test/api/data.json

1、开启serve服务器能查看mock数据

serve （node搭建的服务器）

```shell
npm install -g serve

serve 开启一个服务器 (默认是localhost:5000)

localhost:5000/api/data.json  可获取到mock数据
```

2、mock数据代理转发

```js
// package.json
// 设置
"proxy"：{
	"/api": {
        "target": "http://localhost:5000"
    }
}

localhost:3000/api/data.json  可获取到mock数据
```

方式二：直接将mock数据放到public文件夹

- vscode插件 react-code-snippet    输入rcc能快速生成react代码块