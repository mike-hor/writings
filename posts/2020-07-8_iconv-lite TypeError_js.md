node_modules中，找到iconv-lite，打开iconv-lite/lib/index.js
```tips
注释下面的代码即可
```
```javascript
// Load extensions in Node. All of them are omitted in Browserify build via 'browser' field in package.json.
var nodeVer = typeof process !== 'undefined' && process.versions && process.versions.node;
if (nodeVer) {
 
    // Load streaming support in Node v0.10+
    var nodeVerArr = nodeVer.split(".").map(Number);
    if (nodeVerArr[0] > 0 || nodeVerArr[1] >= 10) {
        require("./streams")(iconv);
    }
 
    // Load Node primitive extensions.
    require("./extend-node")(iconv);
}    
```
