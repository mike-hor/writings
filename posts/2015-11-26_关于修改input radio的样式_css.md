### 关于修改input radio的样式

让label 的for属性与   input radio 的id属性一样 

点击label就相当于设置对应的input check

且在安卓设备中不能直接用透明度隐藏表单 则会扰乱布局 需要直接

```css
display:none

label：befor{

  position:absolute;

  /*点击前的样式*/

}

input[type:radio]:checked + label{

  position:absolute;

/*点击之后的样式*/

}
```
