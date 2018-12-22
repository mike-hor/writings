### node用bable启用最新es特性


#### 全局安装babel-cli 安装babel-register

```
npm install babel-cli -g
npm install babel-register --save
npm install babel-preset-latest --save
npm install babel-plugin-transform-runtime --save-dev
npm install babel-plugin-syntax-object-rest-spread --save-dev
```
#### 安装完之后，还需要添加一个名为.babelrc的配置文件

```
{
  "presets": [
    ["latest", {
      "targets": {
        "node": "current"
      }
    }]
  ],
  "plugins": ["transform-runtime","syntax-object-rest-spread"]
}
```

#### 在项目入口文件（如app.js）引用下babel:

```
require('babel-register')({
    presets: ['es2015']
});
```

