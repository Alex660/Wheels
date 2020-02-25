## 微信小程序中实现混入 mixins
### 定义
+ 混入(mixins)是一种分发页面(Page)可复用功能非常灵活的方式。
+ 简而言之就是在小程序创建页面时，混合页面选项，可以添加钩子功能。 
### code
```javascript
function mixin(...args) {
  let res = {}
  for (let i = 0, j = args.length; i < j; i++) {
    let ob = lodashClonedepp(args[i])
    for (let key in ob) {
      let v = res[key]
      if (v) {
        let t = type(v)
        if (t === "function") {
          res[key] = function () {
            let arg = [].slice.call(arguments)
            ob[key].apply(this, arg)
            return v.apply(this, arg)
          }
        } else if (t === "object" && type(ob[key]) === t) {
          for (let k1 in ob[key]) {
            if (!v.hasOwnProperty(k1)) {
              v[k1] = ob[key][k1]
            }
          }
        }
      } else {
        res[key] = ob[key]
      }
    }
  }
  return res
}
```