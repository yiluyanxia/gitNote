# vue-i18n的粗暴使用

[vue-i18n 文档](https://kazupon.github.io/vue-i18n)  
[vue-i18n GitHub](https://github.com/kazupon/vue-i18n)

## （一）安装

```
npm install vue-i18n
```

## （二）注入 vue 实例中

先在 main.js 中引入 vue-i18n。

```js
import VueI18n from 'vue-i18n'

Vue.use(VueI18n)  // 通过插件的形式挂载

const i18n = new VueI18n({
  locale:'zh-CN',  // 语言标识 使用 this.$i18n.locale 切换语言
  messages:{
    'zh-CN':require('./libs/lang/zh'),
    'en-US':require('./libs/lang/en'),
  }
})

new Vue({
  el: '#app',
  i18n, //还有这里
  router: router,
  store: store,
  components: { App },
  template: '<App/>'
})

```
## （三）开始使用
1. 将对应语言的信息保存为不同的 json对象  

```js
//zh.js
module.exports = {
  images: '图片',
  myImage: '我的图片',
  album:'相册',
  all:'所有',
  others:'其他',
  help:'帮助',
  aboutMe:'关于我'
}
```
```js
//en.js
module.exports = {
  images: 'Images',
  myImage: 'My Images',
  album:'Album',
  all:'All',
  others:'Others',
  help:'Help',
  aboutMe:'About me'
}
```
2. 在模板中使用

```html
<MenuItem name="help">
  <Icon type="help-circled"></Icon>
  {{$t('help')}}
</MenuItem>
```
是 “$t”。

3. 插一句
如果是使用“export const m ”

```js
export const m = {
  images: '图片',
  myImage: '我的图片',
  album:'相册',
  all:'所有',
  others:'其他',
  help:'帮助',
  aboutMe:'关于我'
}
```
则需要写“m.help”

```html
<MenuItem name="help">
  <Icon type="help-circled"></Icon>
  {{$t('m.help')}}
</MenuItem>
```


