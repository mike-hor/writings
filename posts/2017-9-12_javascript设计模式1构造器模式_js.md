### 简单构造器模式的实现   与 原型构造器的优缺点比较

优缺点:一个是难以继承，这不是非常好，理想的情况是所有Person对象都应该共享say这个方法

所以直接在Person的原型链添加say方法最好

```js
var Person = function(name, age) {
    this.name = name;
    this.age = age;
    this.say = function(v) {
        console.log(this.name + 'say: ' + v)
    }
}
Person.prototype = {
    say: function() {
        console.log(this.name + 'say -from:prototype')
    }
}
var xiaoming = new Person('小明', 12);
var xiaohong = new Person('小红', 11);
xiaoming.say('hellow by 小明') //间接说明
console.log(xiaoming);
console.log(xiaohong);
```