---
title: 如果react-amapui是这样的结构，是不是好一点？
date: 2017-11-01 09:50:42
tags:
---

## 这样的结构，会更便利一点？

```
├── index.js                    //对外接口
│   ├── events                  //事件处理，用于处理色彩变化
│   ├── initial                 //初始化
│   ├── render                  //用于渲染
│   │   ├── renderParentFeature //渲染父区域
│   │   ├── renderChildFeature  //渲染子区域
│   ├── willReceiveProps        //用于改变组件的属性
```

还是要学好设计模式啊，感觉看别人东西好tm费劲。

