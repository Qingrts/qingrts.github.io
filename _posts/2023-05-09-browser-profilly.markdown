---
layout: post
title:  "浏览器兼容性问题"
date:   2023-05-09 14:48:00
categories: 前端
tags: 浏览器兼容性
excerpt: 各种兼容性问题
mathjax: true
---

* content
{:toc}

# safari等浏览器 日期问题 NaN
## 问题描述：
Chrome 等浏览器 `Date` 对象支持格式为 `2017-10-14 18:07:27`
Safari 浏览器 `Date` 对象支持格式为 `2017/10/14 18:07:27`

### 解决办法
- 判断浏览器类型，然后替换 `-` 为 `/`
```js
if ((/Safari/.test(navigator.userAgent) && !/Chrome/.test(navigator.userAgent))) {
  if (data.endsWith('.0')) {
    data = data.replace(/\.0/g, '');
  }
  data = new Date(data.replace(/\-/g, '/'));
} else {
  data = new Date(data);
}
```

# toFixed 四舍五入 计算问题
## 问题描述:
1. 注意n的取值为 有范围 超过时就会报错
2. v8引擎采用银行家舍入算法：四舍六入五考虑，五后非零就进一，五后为零看奇偶，五前为偶应舍去，五前为奇要进一
### 解决办法:
```js
// 转换为整数计算后 同比放大 同比缩小 加减乘除 同理
```

