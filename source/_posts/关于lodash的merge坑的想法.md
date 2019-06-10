---
layout: post
title: 关于lodash的merge坑的想法
date: 2017-10-26 11:05:16
tags:
---

## 关于lodash下merge方法的坑

------

该方法是对对象内栈中的内容进行merge，方式如下

```JavaScript
import _ from 'lodash'

const obj0 = {
  propName:'prop_0',
  propNum:0,
  propArray: [0,1],
  propObj: {
    subPropName:'sub_0'
  }
}

const obj1 = {
  propName:'prop_1',
  propNum:1,
  propArray: [0],
  propObj: {
    subPropName:'sub_1'
  }
}

_.merge(obj0,obj1)
```

推测是由于propArray的地址问题，由于地址并没有改变，所以此时obj0下的propArray并不会merge成为[0]。
//具体原因暂未考察，周末之前补充。

