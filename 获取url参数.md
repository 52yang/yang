获取url参数

```JavaScript

/** 获取url参数 **/

function getQueryString(name) {
	var reg = new RegExp("(^|&)" + name + "=([^&]*)(&|$)");
	var r = window.location.search.substr(1).match(reg);
	if( r != null) {
		return unescape(r[2]); 
	}
	return null;
}

// 测试
getQueryString("需要参数的名称");
```
