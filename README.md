# cal-heatmap4-vue2-demo

## Cal-Heatmap

```
https://cal-heatmap.com/docs
```

### cal-heatmap version

```
^4.2.4
```

### 备注

这只是一个简单的使用 vuecli 创建的 vue2 项目。放在诸如 ruoyi 框架中，需要做一些配置。

我在 ruoyi 项目引入 cal-heatmap 过程中踩了很多坑，可能是项目 babel/webpack 配置老旧，但没有找到自认为漂亮的方法。最后是这么解决的 👇

```
// 1. vue.config.js 添加转译 2. 直接引入.esm.js
// vue.config.js
module.exports = {
    transpileDependencies: [/cal-heatmap/], // TODO: calheatmap 让 babel 转译 cal-heatmap
}

// 组件中 这样引用
import CalHeatmap from "cal-heatmap/dist/cal-heatmap.esm.js";
import "cal-heatmap/dist/cal-heatmap.css";
import Tooltip from "cal-heatmap/dist/plugins/Tooltip.esm.js";
import Legend from "cal-heatmap/dist/plugins/Legend.esm.js";
```

## Project setup

```
npm install
```

### Compiles and hot-reloads for development

```
npm run serve
```

### Compiles and minifies for production

```
npm run build
```

### Lints and fixes files

```
npm run lint
```

### Customize configuration

See [Configuration Reference](https://cli.vuejs.org/config/).
