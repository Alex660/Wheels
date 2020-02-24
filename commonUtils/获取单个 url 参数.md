## 获取单个 url 参数
### code
```javascript
var getUrlParam = function(name) {
  var reg = new RegExp("(^|\\?|&)" + name + "=([^&]*)(&|$)");
  var r = window.location.search.match(reg);
  if (r != null) return decodeURIComponent(r[2]);
  return null;
};
```