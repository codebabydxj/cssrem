CSSREM
-------------

一个css-px自动转rem的插件配置 适用v2x，v3x

插件效果如下：

##### 安装

* npm install postcss-px2rem px2rem-loader --save
* yarn add postcss-px2rem px2rem-loader

##### 在根目录src中新建util目录下新建rem.js等比适配文件

```
// rem等比适配配置文件
// 基准大小
const baseSize = 16
// 设置 rem 函数
function setRem () {
  // 当前页面宽度相对于 1920宽的缩放比例，可根据自己需要修改。
  const scale = document.documentElement.clientWidth / 1920
  // 设置页面根节点字体大小（“Math.min(scale, 2)” 指最高放大比例为2，可根据实际业务需求调整）
  document.documentElement.style.fontSize = baseSize * Math.min(scale, 2) + 'px'
}
// 初始化
setRem()
// 改变窗口大小时重新设置 rem
window.onresize = function () {
  setRem()
}
```

##### 在main.js中引入适配文件

```
import '@/util/rem'
```

##### vue.config.js（vue2X）/ vite.config.ts（vue3X）中配置插件

```
// 引入等比适配插件
const px2rem = require('postcss-px2rem') // import px2rem from 'postcss-px2rem';

// 配置基本大小
const postcss = px2rem({
  // 基准大小 baseSize，需要和rem.js中相同
  remUnit: 16
})

// 使用等比适配插件 (vue2x)
module.exports = {
  css: {
    loaderOptions: {
      postcss: {
        plugins: [
          postcss
        ]
      }
    }
  }
}

// 使用等比适配插件 (vue3x)
export default defineConfig({
  plugins: [
    vue()
  ],
  css: {
    postcss: {
      plugins: [
        postcss,
      ]
    }
  },
})
```
