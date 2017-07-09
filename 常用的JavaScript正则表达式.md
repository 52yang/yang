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
