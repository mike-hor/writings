### 实现div从另一个跳出

这个功能是blog中评论按钮点击之后就会跳出评论框 本来用的是框架中的功能 但是感觉比较实用 就自己尝试了下如何实现
#### HTML
```html
<div id="app">
  <div class="contaier">
    <button @click="open">点我</button>
  </div>
  <div class="box-container active">
    <div class="box" :style="styles" :class="{'active':active}">

    </div>
  </div>
</div>
```
#### CSS
```css
.contaier {
  position: fixed;
  top: 100px;
  left: 100px;
  background-color: red;
  width: 400px;
  height: 400px;
}

.box-container {
  display: flex;
  align-items: center;
  pointer-events: none;
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 8;
}

.box {
  overflow: hidden;
  position: absolute;
  left: 0;
  top: 0;
  right: 0;
  bottom: 0;
  margin: auto;
  z-index: 10;
  outline: none;
  border-radius: 2px;
  will-change: opacity, transform;
  width: 200px;
  height: 200px;
  background: black;
  transition: all 0.3s;
  transform-origin: center;
  opacity: 0;
}

.box.active {
  transform: scale(1) !important;
  display: flex;
  opacity: 1!important;
}
```
#### Js
```js
var vm = new Vue({
  el: '#app',
  data: {
    Transform: '',
    active: false
  },
  computed: {
    styles: function() {
      return {
        transform: this.Transform
      }
    }
  },
  mounted: function() {
    this.calculate();
  },
  methods: {
    calculate: function(ref) {
      var FromEl = document.querySelector('.contaier');
      var Element = document.querySelector('.box');
      var FromRect = FromEl.getBoundingClientRect();
      var SelfRect = Element.getBoundingClientRect();
      var widthInScale = FromRect.width / SelfRect.width;
      var heightInScale = FromRect.height / SelfRect.height;
      var SelfRect_Core = {
        top: SelfRect.top + SelfRect.height / 2,
        left: SelfRect.left + SelfRect.width / 2,
      };
      var FromRect_Core = {
        top: FromRect.top + FromRect.height / 2,
        left: FromRect.left + FromRect.width / 2,
      };
      var distance = {
        top: -SelfRect_Core.top + FromRect_Core.top,
        left: -SelfRect_Core.left + FromRect_Core.left
      };
      this.Transform = `translate3D(${distance.left}px, ${distance.top}px, 0) scale(${widthInScale}, ${heightInScale})`;
    },
    open: function() {
      this.active = true;
    }
  }

})
```
#### 最后说下原理
1. 用getBoundingClientRect()获取dom的位置信息
2. 计算出目标与自身的中心点
3. 最后用transform设置,当然还有动画不能忘,具体看看代码就知道了
