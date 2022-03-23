# vue3-ts

在vue3+ts项目中使用eslint+stylint+prettier实现项目规范的模板

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


### 问题记录
**Q:**
Unknown word (CssSyntaxError)错误

**A:**
这个错误是因为安装的插件stylelint``stylelint-config-standard``stylelint-scss版本太新的问题，对于 vue3 模板文件的支持不是很好，不能正确识别.vue文件的 css 代码。所以将以上三个插件的版本降一个大版本就好了，最后的版本如下：
```
"stylelint": "^13.13.1",
"stylelint-config-standard": "^22.0.0",
"stylelint-scss": "^3.21.0",
```
