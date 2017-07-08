原生`ajax`
```JavaScript

/** 原生ajax **/

var ajax = function (options) {
    options = options || {};
    options.type = (options.type || "GET").toUpperCase();
    options.dataType = options.dataType || "json";
    var params = formatParams(options.data);

    //创建 - 非IE6 - 主流浏览器提供了XMLHttpRequest对象
    if (window.XMLHttpRequest) {
        var xhr = new XMLHttpRequest();
    } else {
    	//低版本的IE浏览器没有提供XMLHttpRequest对象，IE6以下
    	//所以必须使用IE浏览器的特定实现ActiveXObject
        var xhr = new ActiveXObject('Microsoft.XMLHTTP');
    }

    //连接 和 发送
    if (options.type == "GET") {
        xhr.open("GET", options.url + "?" + params, true);
        xhr.send(null);
    } else if (options.type == "POST") {
        xhr.open("POST", options.url, true);
        //设置表单提交时的内容类型
        xhr.setRequestHeader("Content-Type", "application/x-www-form-urlencoded");
        xhr.send(params);
    }

    //接收 - readyState 0=>初始化 1=>载入 2=>载入完成 3=>解析 4=>完成
    xhr.onreadystatechange = function () {
        if (xhr.readyState == 4) {
            var status = xhr.status;
            if (status >= 200 && status < 300) {
                options.success && options.success(xhr.responseText, xhr.responseXML);
            } else {
                options.fail && options.fail(status);
            }
        }
    }
}

//格式化参数 --- 处理参数
function formatParams(data) {
    var arr = [];
    for (var name in data) {
        arr.push(encodeURIComponent(name) + "=" + encodeURIComponent(data[name]));
    }
    arr.push(("v=" + Math.random()).replace(".",""));
    return arr.join("&");
}

```
