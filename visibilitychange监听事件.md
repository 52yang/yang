`visibilitychange`监听事件来判断页面可见性，
这个事件可以满足一些用户需求，比如标签页隐藏的时候停止播放音乐视频、停止一些不必要的轮询，还有停止一些诸如轮播等循环动画效果等等。这些可以节省服务器和本地的开销。

```javascript

// visibilitychange监听事件来判断页面可见性，
// 这个事件可以满足一些用户需求，比如标签页隐藏的时候停止播放音乐视频、停止一些不必要的轮询，
// 还有停止一些诸如轮播等循环动画效果等等。这些可以节省服务器和本地的开销。
var visibility = {
	browerKernel: function () {
		var result;
		['webkit', 'moz', 'o', 'ms'].forEach(function (prefix) {
			if (typeof document[ prefix + 'Hidden' ] != 'undefined') {
				result = prefix;
			}
		});
		return result;
	},
	init: function (Callbak) {
		var prefix = this.browerKernel();

		if (Object.prototype.toString.call(Callbak) === '[object Function]') {
			Callbak();
			document.addEventListener(prefix + 'visibilitychange', function (e) {
				Callbak(document[prefix + 'VisibilityState']);
			});
		} else {
			document.title = Callbak;
		}
		
	}
};

// visibility.init()方法的调用与说明
// Callbak是一个回调函数
visibility.init(function (v) {
	document.title = '进入页面';
	if (v == 'visible') {
		document.title = '进入页面';
	} else if (v == 'hidden') {
		document.title = '离开页面';
	}
});


```
