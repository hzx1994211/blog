
```js
##二进制转utf-8
//设置缓冲器
let reader = new FileReader()
//转换成utf-8
reader.readAsText(response.data, "utf-8")
reader.onload = () => {
  let msgInfo = JSON.parse(reader.result)
}
```

