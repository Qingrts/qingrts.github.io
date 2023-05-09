---
layout: post
title:  "调试技巧"
date:   2023-05-09 14:55:00
categories: 调试
tags: chrome 前端
excerpt: 调试技巧
mathjax: true
---

* content
{:toc}


# 前端
## 查看某个元素触发的事件
只需检查您的元素（right mouse click→ Inspect在可见元素上，或转到ElementsChrome开发者工具中的标签并选择所需的元素），然后转到Console标签并编写：
```js
monitorEvents($0);
```
现在，当您将鼠标移到该元素上，进行焦点或单击时，将触发事件的名称及其数据。

要停止获取此数据，只需将其写入控制台：
```js
unmonitorEvents($0);
```

$0只是Chrome开发者工具选择的最后一个DOM元素。您可以在那里传递任何其他DOM对象（例如getElementById或的结果querySelector）。

您还可以将事件“类型”指定为第二个参数，以将监视的​​事件缩小到某个预定义的集合。例如：
```js
monitorEvents(document.body, 'mouse')
```
