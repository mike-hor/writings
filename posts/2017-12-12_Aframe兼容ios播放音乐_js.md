### IOS播放音乐兼容

之前在做AFRAME 的MMD插件的时候遇到兼容问题今天总结下

直接看下面的代码吧

<blockquote class="tip">
iOS 9   还需要额外的 load 一下, 否则直接 play 无效
ios7/8一下直接在点击事件之后Audio.play()即可
</blockquote>

```js
var audioEl = document.getElementById('bgmusic'); //直接new 一个audio一个也可以
//在加载的时候直接赋值src 给Audio 对象
window.addEventListener('touchstart', forceSafariPlayAudio, false); //监听点击事件
//开始播放之后移除事件
audioEl.onplay = function(){
    window.removeEventListener('touchstart', forceSafariPlayAudio, false);
    console.log('移除事件')
}
function forceSafariPlayAudio() {
    audioEl.load(); // iOS 9   还需要额外的 load 一下, 否则直接 play 无效
    audioEl.play(); // iOS 7/8 仅需要 play 一下	                     
}
```