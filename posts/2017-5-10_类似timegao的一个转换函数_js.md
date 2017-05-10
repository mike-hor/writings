### 类似Timeago的一个转换函数

直接上代码,比较简单
<blockquote class="tip">
很久之前写的了 看起来很Low 有时间在改吧
</blockquote>
```js
TranslateTime(time) { 
	var minute = 1000 * 60;
	var hour = minute * 60;
	var day = hour * 24;
	var halfamonth = day * 15;
	var month = day * 30;
	var date = time.substring(0, 19);
	date = date.replace(/-/g, '/').replace(/T/g, ' ').replace(/Z/g, ' '); //转换得到的时间
	var timestamp1 = new Date(date).getTime() + 28800000; //       
	var now = new Date(); // 
	var result;
	var diffValue = now - timestamp1;
	if(diffValue < 0) {
		//alert("结束日期不能小于开始日期！");
	}
	var monthC = diffValue / month;
	var weekC = diffValue / (7 * day);
	var dayC = diffValue / day;
	var hourC = diffValue / hour;
	var minC = diffValue / minute;
	if(monthC >= 1) {
		result = parseInt(monthC) + "个月前";
	} else if(weekC >= 1) {
		result = parseInt(weekC) + "周前";
	} else if(dayC >= 1) {
		result = parseInt(dayC) + "天前";
	} else if(hourC >= 1) {
		result = parseInt(hourC) + "个小时前";
	} else if(minC >= 1) {
		result = parseInt(minC) + "分钟前";
	} else
		result = "刚刚发表";
	return result;
}
```
