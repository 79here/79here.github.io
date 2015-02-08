---
layout: post
title:  Js对象的读写权限控制
date:   2015-02-08 18:10:00
categories: js
---

js对象属性的增加,删除,修改都可控制

- 增加: Object.preventExtensions(O) 

{% highlight javascript %}
var obj = {a:1};
Object.preventExtensions(obj);
obj.b = 2;
console.log(obj); // -> {a:1}
{% endhighlight %}

- 删除: Object.seal(O) 

{% highlight javascript %}
var obj = {a:1};
Object.seal(obj);
delete obj.a
console.log(obj); // -> {a:1}
{% endhighlight %}


- 修改: Object.freeze(O) 
{% highlight javascript %}
var obj = {a:1};
Object.freeze(obj);
obj.a = 2;
console.log(obj); // -> {a:1}
{% endhighlight %}

以上都是针对对象级的控制,针对单个的属性如何控制呢?答案如下:
`Object.defineProperty(O,Prop,descriptor)`

O对象, Prop属性名, descriptor属性配置,是一个键值对,具体描述如下:

1. value: 值,默认undefined
2. writable：是否可写，默认是false
3. enumerable：是否可以被枚举(for in)，默认false
4. configurable：是否可以被删除，默认false