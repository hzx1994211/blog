
```nuxt
1.Nuxt引用cookie-universal-nuxt在服务端请求cookie

npm install cookie-universal-nuxt -s

在nuxt.config.js添加
 modules: [
    'cookie-universal-nuxt'
  ],

设置cookie
this.$cookies.set('token', 123456)

获取cookie
this.$cookies.get("token")

清除cookie
this.$cookies.remove('token')


在asyncData获取
async asyncData({ app }) {
    console.log(app.$cookies.get("token"));
},
https://blog.csdn.net/AK852369/article/details/115792191 //参考资料
```

