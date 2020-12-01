# Typescript

配置ts项目流程

1.安装ts    npm i typescript -g

2。tsc -init   初始化tsc配置文件tsconfig.json

3.修改tsconfig.json中的

"target": "es5", 解析成js后的版本

"module": "amd"  模块的类型，用于网页使用amd。用于node使用

"outDir" : "./js/"  解析后的文件夹

## typescript基础

### 基础类型

###### 布尔值

```js
let a:boolean=false;
```

