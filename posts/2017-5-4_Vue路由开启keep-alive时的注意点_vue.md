### Vue路由开启keep-alive时的注意点

最近用了vue2.0的keep-alive  看了网上的资料有些问题总结下

1. 生命周期

钩子的触发顺序created-> mounted-> activated，退出时触发deactivated。当再次进入（前进或者后退）时，只触发activated。

<blockquote class="tip">
所以，应该activated中留一份数据获取的代码，或者不要created部分，直接将created中的代码转移到activated中。

但是这个博客中的文章都是在本地进行了缓存,所以访问一次后是不需要在获取数据的 所以我是直接在created阶段获取的数据
</blockquote>

2. 另一个是关于 $route 中的数据读不到

以前的写法是在data中将需要的 $route 数据进行赋值，便于其余方法使用，但是使用了 keep-alive 后数据需要进入页面在activated中再次获取，才能达到更新的目的。定义一个initData方法，然后在activated中启动。

```js
initData: function () {

        let _this = this;

        _this.fromLocation = JSON.parse(this.$route.query.fromLocation);

        _this.toLocation = JSON.parse(this.$route.query.toLocation);

        _this.activeIndex = parseInt(this.$route.params.activeIndex) || 0;

        _this.policyType = parseInt(this.$route.params.policyType) || 0;

},
```
3. 另一个是当页动态修改url

这个我和网上处理方法不同,我是自己本地在locaStronge处理的

4. 事件多吃绑定问题

只需要在mounted中绑定一次即可
