### 关于1.5 Tiled 地图动态创建刚体中创建多边形碰撞体的小坑

首先单独的创建简单碰撞体应该基本没问题 可以参照

[1.5 自动计算tilemap中图层为物理引擎刚体的方法](http://forum.cocos.com/t/1-5-tilemap/46779/6)

主要是创建多边形 直接贴代码看注释吧

```js
var sfloors = this.tiledMap.getObjectGroup('Special_Floor').getObjects(); //此处获取对象层
for (let i = 0, l = sfloors.length; i < l; i++) {
    let sfloorsgNode = sfloors[i];
    let compoent = this.floor_physics.addComponent(cc.PhysicsPolygonCollider);
    let poitlist = sfloorsgNode.getProperties().points
     //一个是在这 getProperties   找了很久都没找到这个points的属性结果没在shNode上,而且这个方法也是隐藏得很深 文档根本没有???
    compoent.points = [];
    for (var index = 0; index < poitlist.length; index++) {      
        poitlist[index].y = -poitlist[index].y;//翻转碰撞体
        compoent.points.push(cc.p(poitlist[index]));              
    }
    compoent.offset = new cc.p(sfloorsgNode.sgNode.x, sfloorsgNode.sgNode.y);
}
```