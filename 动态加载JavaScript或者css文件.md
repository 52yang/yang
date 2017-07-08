动态加载JavaScript

```JavaScript

// 方法一：动态加载js文件
// 动态加载js脚本文件
function loadScript(url) {
    var script = document.createElement("script");
    script.type = "text/javascript";
    script.src = url;
    document.body.appendChild(script);
}
// 测试
loadScript("javascript/lib/cookie.js");

// 方法二：动态加载js文件
// 动态加载js脚本
function loadScriptString(code) {
    var script = document.createElement("script");
    script.type = "text/javascript";
    try{
        // firefox、safari、chrome和Opera
        script.appendChild(document.createTextNode(code));
    }catch(ex) {
        // IE早期的浏览器 ,需要使用script的text属性来指定javascript代码。
        script.text = code;
    }
    document.body.appendChild(script);
}
// 测试
var text = "function test(){alert('test');}";
loadScriptString(text);
test();

```

动态加载css

```JavaScript

// 方法一：动态加载css文件
// 动态加载css文件
function loadStyles(url) {
    var link = document.createElement("link");
    link.type = "text/css";
    link.rel = "stylesheet";
    link.href = url;
    document.getElementsByTagName("head")[0].appendChild(link);
}
// 测试
loadStyles("css/secondindex.css");

// 方法二：动态加载css文件
// 动态加载css脚本
function loadStyleString(cssText) {
    var style = document.createElement("style");
    style.type = "text/css";
    try{
        // firefox、safari、chrome和Opera
        style.appendChild(document.createTextNode(cssText));
    }catch(ex) {
        // IE早期的浏览器 ,需要使用style元素的stylesheet属性的cssText属性
        style.styleSheet.cssText = cssText;
    }
    document.getElementsByTagName("head")[0].appendChild(style);
}
// 测试
var css = "body{color:blue;}";
loadStyleString(css);

```
