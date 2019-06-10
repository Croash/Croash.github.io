---
title: 关于redux-saga的一点想法
date: 2018-03-22 18:00:04
tags: 杂
---

## redux-saga的暗坑和一些用法

1. redux-saga环中环之无限循环
在调用一次saga之后，如果在saga中仍然有reducer的出现，会再一次调用saga，如果不进行拦截，会导致页面无限循环，卡死在这里。

```js
//reducer
let updateData = ()=>{ dispatch({ type:'update', payload:{ data:'data'} ) }

//saga
let saga = function* {
  yield takeEvery(action=>action.type=='update',sagaFunc)
}

//sagaFunc
let sagaFunc = function* {
  yield put({ type:'update',payload:{ sg:'sg' } })
}
```

ok, 只要你这么搞，页面就会无限卡死在saga调用reducer然后再次触发saga的奇妙状态下。

2. 如何解决无限循环
那么怎么处理呢，需要简单的处理一下saga和sagaFunc的写法。

```js
//saga
let saga = function* {
  yield [takeEvery(action=>action.type=='update',sagaFunc),
  takeEvery(action=>action.type=='update'&&['sagaKey'].indexOf(action.key)>0,sagaFunc
  ]
}

//sagaFunc
let sagaFunc = function* {
  yield put({ type:'update',payload:{ sg:'sg' }, key:'sagaKey' })
}
```

这样就成功拦截了之前没有key的reducer，就不会有无限循环了。

## saga的意义

这两天想了一下，redux-saga的意义其实在于将前端进行进一步解耦。
redux的意义在于，将重逻辑从组件中剥离出来，而saga的意义在于，将许多边界条件进行细分处理。
怎么说呢，用着应该会非常的爽（因为暂时还没开始用）

## poker2 键盘的使用感受

最近买了一把 poker2 红轴键盘，打字轻便，我觉着终于获得了打字的快感，原来的话...应该是每天想东西更多一点（才怪
红轴讲道理，是比黑轴的好用，黑轴还是太重了，写多了手指会累，尤其是大拇指。
可编程这一点非常棒，像我就用了一些之前习惯的按键，比如\`放到了esc上（然后就可以开心的``` `${abc}` ```）。但是悲剧的是，默认的fn加esc我不知道怎么弄成esc，所以只能将esc的功能放到fn加q上了。

## switch 到货了

商家真是良心，胶带纸我解了20分钟才解开，不过想想待会儿就可以去玩我的马里奥，这点苦算什么呢
