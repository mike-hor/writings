### 发布订阅模式 与 观察者模式

主要用于全局只有一个对象的时候,无论如何实例化都返回相同的实例

#### 区别

最大的区别是调度方式的不同。

##### 发布/订阅模式
在JavaScript的生态系统中非常合适，主要是因为作为核心的ECMAScript 实现是事件驱动的。
尤其是在浏览器环境下更是如此，因为DOM使用事件作为其主要的用于脚本的交互API。

##### 观察者模式
观察者模式的订阅者与发布者之间是存在依赖的
每一个发布者自己维护一个观察者列表[]列表中是各个需要通知的订阅者对象 然后当触发了事件就直接通知所有
的订阅者(即运行updata方法)

```js
/*--------------------------发布/订阅模式-----------------------------------*/
function Event() {
    var handlist = {};
    return {
        on: function(eventName, fn) {
            if(handlist[eventName]) {
                handlist[eventName].push(fn);
            } else {
                handlist[eventName] = [];
                handlist[eventName].push(fn);
            }
        },
        gethandlist: function() {
            return handlist
        },
        // 触发事件 eventName   当arg是多个参数时 需要传递数组作为参数！！！！
        trigger: function(eventName, args) {
            if(handlist[arguments[0]]) {
                for(var i = 0; i < handlist[arguments[0]].length; i++) {
                    if(arguments.length > 2) {
                        var arg = Array.prototype.slice.call(arguments,1);
                        handlist[arguments[0]][i].apply(this, arg);

                    } else {
                        handlist[arguments[0]][i].call(this, args);
                    }
                }
            } else {
                console.error('eventName:' + eventName + 'not to found')
            }
        },
        delete: function(eventName) {
            delete handlist[eventName]
        }
    }
}
var event = new Event();
event.on('abc.show', function(a, b, c) {
    console.log('abc.show')
    console.log(a, b, c)
})
event.on('abc.show', function(a, b, c) {
    console.log('abc.show2')
    console.log(a, b, c)
})
event.trigger('abc.show', 1, 2, 3)
/*---------------------------------观察者模式------------------------------------------------*/
//观察者列表
function ObserverList() {
    this.observerList = [];
}
ObserverList.prototype.add = function(obj) {
    return this.observerList.push(obj);
};
ObserverList.prototype.count = function() {
    return this.observerList.length;
};
ObserverList.prototype.get = function(index) {
    if(index > -1 && index < this.observerList.length) {
        return this.observerList[index];
    }
};
ObserverList.prototype.indexOf = function(obj, startIndex) {
    var i = startIndex;
    while(i < this.observerList.length) {
        if(this.observerList[i] === obj) {
            return i;
        }
        i++;
    }
    return -1;
};
ObserverList.prototype.removeAt = function(index) {
    this.observerList.splice(index, 1);
};
// 合并对象
function extend(extension, obj) {
    for(var key in extension) {
        obj[key] = extension[key];
    }
}
//目标
function Subject() {
    this.observers = new ObserverList();
}
Subject.prototype.addObserver = function(observer) {
    this.observers.add(observer);
};
Subject.prototype.removeObserver = function(observer) {
    this.observers.removeAt(this.observers.indexOf(observer, 0));
};
Subject.prototype.notify = function(context) {
    var observerCount = this.observers.count();
    for(var i = 0; i < observerCount; i++) {
        this.observers.get(i).update(context);
    }
};

//观察者
function Observer() {
    this.update = function(context) {

    };
}
// 我们DOM 元素的引用

var controlCheckbox = document.getElementById("mainCheckbox"),
    addBtn = document.getElementById("addNewObserver"),
    container = document.getElementById("observersContainer");

// 具体的被观察者

// 合并对象
extend(new Subject(), controlCheckbox);


//点击checkbox 将会触发对观察者的通知
controlCheckbox.onclick = function() {
    controlCheckbox.notify(this.checked)
};

//添加一个观察者
addBtn.onclick = AddNewObserver;


// 具体的观察者

function AddNewObserver() {
    //建立一个新的用于增加的checkbox
    var check = document.createElement("input");
    check.type = "checkbox";

    // 合并对象
    extend(new Observer(), check);

    // 复写update的方法
    check.update = function(value) {
        this.checked = value;
    };

    // 增加新的观察者到我们主要的被观察者的观察者列表中
    controlCheckbox.addObserver(check);

    // 将元素添加到容器的最后
    container.appendChild(check);

}
```
