# 部分安卓机上rem计算错误导致的布局问题

> &copy; suny 2017-06-27

### 问题描述

　　在移动端采用rem布局方案，发现在部分安卓机型的微信中打开页面时，页面的宽度大于viewport的宽度，导致布局失真。

### 问题分析

1). rem布局方案为js动态设置html元素的font-size属性。




	<script type="text/javascript">
	    (function (doc, win) {
	        var docEl = doc.documentElement,
	            resizeEvt = 'orientationchange' in window ? 'orientationchange' : 'resize',
	            recalc = function () {
	                var clientWidth = docEl.clientWidth;
	                if (!clientWidth) return;
	                if(clientWidth>750){
	                    clientWidth = 750;
	                }
	                docEl.style.fontSize = 100*(clientWidth/750)+'px';
	            };
	        if (!doc.addEventListener) return;
	        win.addEventListener(resizeEvt, recalc, false);
	        doc.addEventListener('DOMContentLoaded', recalc, false);
	    })(document, window);
	</script>

　




2). 选择一个以rem为单位设置宽度的DOM元素，用js获取其宽度，与预期值进行比较。

- 选取某元素（设计稿宽度为expectWidth,单位px）
- 计算rem值（remWidth = expectWidth / 100）
- 样式编码（使用rem设置宽度）
- js获取宽度（realWidth = ele.clientWidth）

> 宽度与期望值不符，比预期的值要大。即 realWidth > expectWidth

3). 观察页面发现，页面中采用rem设置尺寸的元素没有变形，只是整体放大了。

> 说明rem布局虽然异常了，但是是按照固定比值异常的

4). 由2)可知，其实对于每部异常的手机，这个异常比值是可以计算出来的。

> fitRadio = realWidth / expectWidth

5). 既然比值可以得到，那是不是可以把这个异常扩大（或缩小）的尺寸量再缩（放）回去...

> 由于正常情况下realWidth 与 expectWidth也有可能存在一些微小的差异，所以需要设置一个阀值，只有差异超过这个阀值才重置html元素的font-size属性。

6). 由上得出安卓机上rem适配的兼容方案


	<script type="text/javascript">
	    (function (doc, win) {
	        var docEl = doc.documentElement,
	            resizeEvt = 'orientationchange' in window ? 'orientationchange' : 'resize',
	            recalc = function () {
	                var clientWidth = docEl.clientWidth;
	                if (!clientWidth) return;
	                if(clientWidth>750){
	                    clientWidth = 750;
	                }
	                docEl.style.fontSize = 100*(clientWidth/750)+'px';
	                adjustRem(docEl, clientWidth);
	            };
	        function adjustRem (docEl, clientWidth) {
	            if (!clientWidth || clientWidth >= 750) return;
	            var div = document.createElement('div');
	            div.style.width = '1.5rem';
	            div.style.height = '0';
	            document.body.appendChild(div);
	            var expectWidth = 140 * clientWidth / 750;
	            var fitRadio = (div.clientWidth / expectWidth);
	            if(fitRadio > 1.1 || fitRadio < 0.9){
	                docEl.style.fontSize = 100 * (clientWidth / 750) / fitRadio + 'px';
	            }
	            document.body.removeChild(div);
	        }
	        if (!doc.addEventListener) return;
	        win.addEventListener(resizeEvt, recalc, false);
	        doc.addEventListener('DOMContentLoaded', recalc, false);
	    })(document, window);
	</script>



### 问题总结

待总结...




