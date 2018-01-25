### 暴露模块模式

主要用于全局只有一个对象的时候,无论如何实例化都返回相同的实例

#### 优势

在这个模式中统一返回相同的实例,让操作不会作用于其他的实例，保证操作作用于同一对象

#### 缺点

会增加程序的耦合程度

```js
//实现一个全局模态窗口
var Modal = (function() {
    var _instance = null;
    var _show = false;
    function modal() {
        return {
            toggleModal: function() {
                _show = !_show;
                console.log('当前状态' + (_show ? '显示' : '隐藏'));
            },
            state: function() {
                return _show
            }
        }
    }
    // 获取实例
    return function() {
        // 如果没有创将创建并保存其实例
        if(!_instance) {
            _instance = new modal();
        }
        // 返回实例
        return _instance;
    }
}())
var modal1 = new Modal();
var modal2 = new Modal();
console.log(modal1 === modal2) //true
```
