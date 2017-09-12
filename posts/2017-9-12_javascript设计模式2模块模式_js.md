### 模块模式

使用返回一个立即执行函数(IIFE)

模块模式使用闭包的方式来将"私有信息",状态和组织结构封装起来。提供了一种将公有和私有方法，

变量封装混合在一起的方式，这种方式防止内部信息泄露到全局中，从而避免了和其它开发者接口发生冲图的可能性。

<blockquote class="tip">

模块模式的缺点是因为我们采用不同的方式访问公有和私有成员，因此当我们想要改变这些成员的可见性的时候，我们不得不在所有使用这些成员的地方修改代码。

</blockquote>

```js
var moudleA = (function(w) {
    var counter = 0; //私有变量
    var _sayhellow = function() {
        console.log(counter)
    } //私有方法 只有内部可调用
    return {
        name: 'moudleA', //公有变量
        incrementCounter: function() {
            return counter++;
        },
        sayhellow: _sayhellow,
        showCounter: function() {
            console.log("counter is: " + counter);
        }
    };
})(window)
console.log(moudleA)
moudleA.showCounter(); //counter value prior to reset: 0
moudleA.incrementCounter(); //couter+1
moudleA.showCounter(); //counter value prior to reset: 1
moudleA.sayhellow();
```