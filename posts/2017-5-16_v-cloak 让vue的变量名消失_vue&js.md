### v-cloak 让vue的变量名消失

之前没注意这个用法今天才知道,- -!,之前写的hybrid App 就有个问题 页面加载太快会出现变量名

当时简单的处理是 延迟一点显示

现在直接说下用法

在你需要的的代码上添加

```html
<ul v-cloak v-for="(item,index) in items">
  <li>{{ item.title }}</li>
</ul>
```

如上面的代码添加一个**v-cloak**

然后添加css

```css
[v-cloak] {
  display: none;
}
```

一开始该列表就会隐藏之后等vue ready v-cloak 属性会被自动去除动

这样就不会直接出现那些类似**{{item.title}}**的代码了

<blockquote class="tip">
需要记住的一点是 上面的样式不要由@import 加载css文件进来 需要直接写link的css中
</blockquote>

