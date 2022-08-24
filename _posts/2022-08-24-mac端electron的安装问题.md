---
layout:     post
title:     	electron的安装问题
subtitle: 	mac安装electron遇到的问题
date:       2022-08-22
author:     疏影
header-img: img/home-bg-o.jpg
catalog: true
tags:
    - electron
    - vue
---

# 前言
>之前工作中第一次接触到了electron这个东西，并且发现ff工具的<font color=blue>鱼糕</font>和<font color=blue>配方计算器</font>都是用这东西做的，顿时来了兴致想装来玩一玩，安装过程中遇到了几个问题，简要说下留做记录。

### vue ui
之前我一直觉得图形化界面虽然很方便，但是对于开发经验不多的我不利于学习，容易造成偷懒的毛病。但是这东西集成化程度确实很高，后面我用命令行安装的时候遇到的几个问题，用vue-ui都没有遇到，一次就安装成功了。。。我也不知道这是好事还是坏事

### No Xcode or CLT version detected!
随后开始尝试命令行安装，遇到了第一个问题：Xcode检测不到版本。Bing了一下发现大部分原因是mac系统升级这个命令行工具没有随之升级，需要删除原先的库重新安装。
话不多说开始重装
```
xcode-select --print-path
/Library/Developer/CommandLineTools
```
先找到Xcode的路径，一般路径都是这个
```
sudo rm -r -f /Library/Developer/CommandLineTools
//删除原先的库
sudo xcode-select --install
//重新安装
```
随后会弹窗让你同意协议，同意之后等个十来分钟左右就安装好了，至此完成

### Cannot find module 'fs/promises'
这个查了下说是因为cnpm和node版本不匹配造成的，node高版本promises的引入方式变了，简单来说就是要么你node升级，要么你cnpm降级。虽然我用的是npm，但可能用的也是淘宝镜像所以也会报这个错吧，maybe。
我选择升级node，之前的node一直是12.19版本的，既然以后用vue3还是升级node比较好。
```
npm cache clean -f
//这一步是清除之前的npm缓存 他还会报告警"I sure you know what are you doing"
sudo npm install -g n
//全局安装node版本管理工具
sudo n stable
//不是大潮吧当然选择稳定版
```
解决之后最好把刚创建的项目删了重新创建一个，否则可能会遇到装好electron-builder却无法启动的情况
![package.json里显示了依赖却还是找不到](/img/2022-08-22-error.png)