1.判断是否全由数字组成
```javascript
var isDigit = function (s) { 
    var patrn = /^[0-9]{1,20}$/; 
    if (!patrn.exec(s)) return false;
    return true;
}
```
2.计算字符串的长度（一个双字节字符长度计2，ASCII字符计1）
```javascript
String.prototype.len = function () { return this.replace([^x00-xff]/g, "aa").length; }
```
3.去除左右两边空格
```javascript
var trim = function (s) {
    return s.replace(/(^\s*)|(\s*$)/g, '');
}
```
4.去除左边空格
```javascript
var trimLeft = function (s) {
    return s.replace(/(^\s*)/g, '');
}
```
5.去除右边空格
```javascript
var trimRight = function (s) {
    return s.replace(/(\s*$)/g, '');
}
```
6.取得url上的查询参数，{name:value}格式，如：Url.query.id取得url上id=123的值即返回123（PS：这个是在花满楼的博客上找到的）
```javascript
var Url = function (loc) {
    var urlUtils = function () {
        return {
            trim : function (url) {
                return url.replace(/^\s+|\s+$/,'');
            },
            norProtocol : function (url) {
                if (!/https?\:\/\//i.test(url)) throw url+' http or https protocol needed !';
                return url.replace(/(https?\:\/\/)\/+/,'$1');
            },
            getProtocol : function (url) {
                return this.norProtocol(url).match(/(https?\:\/\/)/)[1];
            },
            tryOnce : function (url) {
                return this.getProtocol(url) + 
                       this.norProtocol(url).substring(this.getProtocol(url).length)
                       .replace(/\.+(?=\/)/g,'')
                       .replace(/\/+/g,'/');
            },
            normalize : function (url) {
                var nor = this.tryOnce(this.trim(url));
                return nor.match(/https?\:\/\/(\w+(?:\.\w+)+)(\:\d{2,5})?$/)?nor+='/':nor;
            },
            isAccessUrl : function (url) {
                return /https?\:\/\/(?:\w+(?:\.\w+)+|localhost)(?:\:\d{2,5})?\/\S*/i.test(this.normalize(url));
            },
            convertQs : function (qs) {
                var qs = qs || loc.search.substring(1);
                if (!qs) return null;
                var qsArr = qs.split(/&/), qsPar = {};
                for (var i = 0; i < qsArr.length; i++){
                    if (qsArr[i]) {
                        var nm = qsArr[i].split(/=/);
                        qsPar[decodeURIComponent(nm[0])] = decodeURIComponent(nm[1]||'');
                    }
                }
                return qsPar;
            }
        }
    }();
    function parse(url) {
        var url = url || loc.href;
        var noredUrl = urlUtils.normalize(url);
        if (!urlUtils.isAccessUrl(url)) throw url+' is not access URI !';
        var medUrl = noredUrl.match(/https?\:\/\/(\w+(?:\.\w+)+|localhost)(?:\:(\d{2,5}))?(\/(?:[^#?]+)?)(?:\?([^#]+))?(?:#{1}(.+))?/i);
        console.log(medUrl)
        return {
            href : medUrl[0],
            protocol : urlUtils.getProtocol(noredUrl).replace(/\/\//,''),
            query : urlUtils.convertQs(medUrl[4]),
            host : medUrl[1],
            port : medUrl[2]||'80',
            pathname : medUrl[3],
            search : medUrl[4]||null,
            hash : medUrl[5]||null
        };
    }
    return {
        parse : parse,
        normalize : urlUtils.normalize,
        isAccessUrl : urlUtils.isAccessUrl,
        query : urlUtils.convertQs(null)      //{name:value}
    }
}(location);

```

未完待续······
