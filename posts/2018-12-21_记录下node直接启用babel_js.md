### node用bable启用es8特性


#### 全局安装babel-cli， 项目安装 babel-preset-es2017:

```
npm install babel-cli -g
npm install babel-preset-es2017 --save
```
#### 安装完之后，还需要添加一个名为.babelrc的配置文件

```
{
  "presets": ["es2017"],
  "plugins": [
    "add-module-exports"
  ]
}
```

#### 在项目入口文件（如app.js）引用下babel:

```
require('babel-register')({
    presets: ['es2015']
});
```

