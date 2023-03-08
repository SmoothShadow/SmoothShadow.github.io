---
layout:     post
title:     	vue组件不识别及环境变量报错问题
subtitle: 	vite+ts搭建过程中踩坑之一
date:       2023-03-08
author:     疏影
header-img: img/home-bg-o.jpg
catalog: true
tags:
    - vite2
    - vue3
    - ts
    - 学习
---

# 前言
>最近在学习vite和ts,把学习过程中遇到的问题记录下来方便以后回顾.

### vue组件不识别的问题
不同于vue2,在vue3+ts的环境中引入.vue文件会产生报错:
![无法识别.vue文件](/img/2023-03-08-error.png)
我创建的vite项目是默认没有shims.d.ts文件的,需要自己在src目录下新建shims.d.ts文件,然后在文件中写入以下代码:
```
//解决不识别ts文件中引入.vue文件报错问题
declare module "*.vue" {
  import { defineComponent } from "vue";
  const Component: ReturnType<typeof defineComponent>;
  export default Component;
 }
```
保存后所有的.vue不再报错
### 找不到对应模块
在解决上面问题时还出现了使用环境变量的代码提示找不到对应模块的报错,
在tsconfig.json中的‘compilerOptions’中添加以下代码:
```
// 解决vue组件内使用环境变量提示找不到对应文件的问题
  "baseUrl": ".",
  "paths": {
    "@/*": [ "src/*" ],
  }
```
实测写入该代码后此问题不再出现