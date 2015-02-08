---
layout: post
title:  dom事件模型
date:   2015-02-09 21:20
categories: js
---

![](/theme/domEvent_bubble.gif)

1. 事件分为捕获阶段(父->子)和冒泡阶段(子->父)
2. IE不支持捕获,现代浏览器则为先捕获再冒泡
3. 现代浏览器中,若触发了一个事件,则先捕获再冒泡遍历dom,则dom上绑定了该事件,则触发该句柄
4. 用addEventListener绑定事件监听,第3个参数为true,则在捕获阶段触发

#### jQuery 中bind(),live(),delegate(),on() 区别	

- bind会为每个元素绑定句柄(不支持动态绑定)
- live利用冒泡原理,在document做代理(已经废弃)
- delegate和live类型,但可以指定代理节点(更快相应)
- on以上方法都是用on实现的
{% highlight javascript %}
jQuery.fn.extend({
	hover: function( fnOver, fnOut ) {
		return this.mouseenter( fnOver ).mouseleave( fnOut || fnOver );
	},

	bind: function( types, data, fn ) {
		return this.on( types, null, data, fn );
	},
	unbind: function( types, fn ) {
		return this.off( types, null, fn );
	},

	delegate: function( selector, types, data, fn ) {
		return this.on( types, selector, data, fn );
	},
	undelegate: function( selector, types, fn ) {
		// ( namespace ) or ( selector, types [, fn] )
		return arguments.length === 1 ? this.off( selector, "**" ) : this.off( types, selector || "**", fn );
	}
});
{% endhighlight %}