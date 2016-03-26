# NodeV-clicent

> express+vue中的vue 

## 项目介绍

这哪是什么鬼项目啊...

个人无聊，作怪，听了组长的idea，做的一个查看git用户信息，以及他star过的项目的烂尾。我居然还加上了登录注册...

目前还缺一个功能点 给star过的项目加标签（就是分类），可以给自己的，也可以给别人的。

最近有点懒，不想写，就先搁着，我先去拯救cndota...

## 开发环境配置

开发过程中vue-cli会建立一个简易的express服务器（不同于NodeV-server中的express）以支持开发过程中的热加载等技术，因此同时开发服务端的Node时，需要解决跨域请求的问题

build文件夹中的dev-server可以自己设置转发请求的端口号

```
var proxyTable = {
  '/api': {
    target: 'http://localhost:3000',
    changeOrigin: true
  }
}
```

前后端如果需要同时开发，请将target的值修改成Node服务端的url值

## 生产环境配置

生产环境下请将webpack.base.conf.js的输出路径写成Node端模板输出的静态文件夹中。

```
output: {
    path: path.resolve(__dirname, '../../server/public'),
    publicPath: '/static/',
    filename: '[name].js'
  }
```


## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# run unit tests
npm test
```

