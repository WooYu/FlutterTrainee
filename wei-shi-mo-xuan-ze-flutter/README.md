---
description: Flutter 是 Google 开源的应用开发框架，仅通过一套代码库，就能构建精美的、原生平台编译的多平台应用，涵盖移动、Web、桌面和嵌入式。
---

# 为什么选择Flutter

## 背景和问题

1、原生开发成本高，不同平台需要找不同的技术人员。



## 问题方案的选择

<img src="../.gitbook/assets/file.excalidraw.svg" alt="跨平台方案" class="gitbook-drawing">

### 方案一：WebView

> 最早出现的跨平台框架是基于JavaScript和WebView，代表框架有PhoneGap，Apache Cordova，Ionic等。
>
> **实现方式：**
>
> 原生的网页加载控件 WebView (Android)或 WKWebView（ios）来加载H5构建的页面，本地的一些服务【比如蓝牙、相机等】需要调用JavaScript进行桥接，调用Native的一些代码来完成某些功能。
>
> **优点：**
>
> 开发成本低，版本升级容易，前端开发可以直接入手；
>
> **缺点：**
>
> 无法调用系统级的 API；
>
> 性能和体验比较差，体验受限于网络环境、渲染性能、平台特性、浏览器等因素；
