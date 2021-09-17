#### canvas

画布。
canvas.

**属性说明**
**Property description**

|属性名|类型|默认值|说明|
| Attribute name | Types of    | Defaults | Description                                                  |
|:-|:-|:-|:-|
|canvas-id|String||canvas 组件的唯一标识符|
| canvas-id      | String      |          | The unique identifier of the canvas component                |
|disable-scroll|Boolean|false|当在 canvas 中移动时且有绑定手势事件时，禁止屏幕滚动以及下拉刷新|
| disable-scroll | Boolean     | false    | When moving in the canvas and there are bound gesture events, prohibit screen scrolling and pull-down refresh |
|@longtap|EventHandle||手指长按 500ms 之后触发，触发了长按事件后进行移动不会触发屏幕的滚动|
| @longtap       | EventHandle |          | Triggered after a long finger press for 500ms, moving after the long press event is triggered will not trigger the scrolling of the screen |
|@error|EventHandle||当发生错误时触发 error 事件，detail = {errMsg: 'something wrong'}|
| @error         | EventHandle |          | The error event is triggered when an error occurs, detail = {errMsg:'something wrong'} |

**注意事项：**
**Precautions:**

* canvas 标签默认宽度 300px、高度 225px，动态修改 canvas 大小后需要重新绘制。
* The canvas tag has a default width of 300px and a height of 225px. It needs to be redrawn after dynamically changing the canvas size.
* h5、app-vue 中单个尺寸过大的 canvas 在 iOS/Safari 无法绘制（具体限制尺寸未公布）。
* In h5 and app-vue, a single canvas whose size is too large cannot be drawn on iOS/Safari (the specific size limit has not been announced).
* 同一页面中的 canvas-id 不可重复，如果使用一个已经出现过的 canvas-id，该 canvas 标签对应的画布将被隐藏并不再正常工作。
*  The canvas-id in the same page cannot be repeated. If a canvas-id that has already appeared is used, the canvas corresponding to the canvas tag will be hidden and no longer work normally.
* 解决 canvas 层级过高无法覆盖，参考 [native-component](/component/native-component)。
* To solve the problem that the canvas level is too high to cover, please refer to [native-component](/component/native-component).
* app-vue 中的 canvas 仍然是 webview 的 canvas。app-nvue下如需使用canvas，需下载插件，详见文档底部章节。
*  The canvas in app-vue is still the canvas of webview. If you need to use canvas under app-nvue, you need to download the plug-in, see the chapter at the bottom of the document for details.
* app-vue的canvas虽然是webview自带的canvas，但却比nvue的原生canvas性能更高。注意并非原生=更快。canvas动画的流畅，关键不在于渲染引擎的速度，而在于减少从逻辑层向视图层频繁通信造成的折损。
*  Although the canvas of app-vue is the canvas that comes with webview, it has higher performance than the native canvas of nvue and WeChat applets. Note that not native = faster. The key to the smoothness of canvas animation is not the speed of the rendering engine, but the reduction of the loss caused by frequent communication from the logic layer to the view layer.
* app-nvue，因为通信阻塞，难以绘制非常流畅的canvas动画。h5和app-vue不存在此问题。但注意，app-vue下若想流畅的绘制canvas动画，需要使用[renderjs](https://uniapp.dcloud.io/frame?id=renderjs)技术，把操作canvas的js逻辑放到视图层运行，避免逻辑层和视图层频繁通信。hello uni-app的canvas示例很典型，在相同手机运行该示例，可以看出在h5端和app端非常流畅，而小程序端由于没有renderjs技术，做不到这么流畅的动画。
* Small programs and app-nvue, because of communication blockage, it is difficult to draw very smooth canvas animation. h5 and app-vue do not have this problem. But note that if you want to draw canvas animation smoothly under app-vue, you need to use [renderjs](https://uniapp.dcloud.io/frame?id=renderjs) technology to put the js logic that operates the canvas in the view layer to run, avoiding frequent communication between the logic layer and the view layer. The canvas example of hello uni-app is very typical. Running the example on the same mobile phone shows that it is very smooth on both the h5 and app sides, while the applet terminal cannot achieve such smooth animation because it does not have renderjs technology.

**示例：** [查看演示](https://hellouniapp.dcloud.net.cn/pages/component/canvas/canvas)
**Example:** [View Demo](https://hellouniapp.dcloud.net.cn/pages/component/canvas/canvas)
 
```html
<template>
	<view>
		<canvas style="width: 300px; height: 200px;" canvas-id="firstCanvas" id="firstCanvas"></canvas>
		<canvas style="width: 400px; height: 500px;" canvas-id="secondCanvas" id="secondCanvas"></canvas>
		<canvas style="width: 400px; height: 500px;" canvas-id="secondCanvas" id="secondCanvas" @error="canvasIdErrorCallback"></canvas>
	</view>
</template>
```
 
```javascript
export default {
	onReady: function (e) {
		var context = uni.createCanvasContext('firstCanvas')
		context.setStrokeStyle("#00ff00")
		context.setLineWidth(5)
		context.rect(0, 0, 200, 200)
		context.stroke()
		context.setStrokeStyle("#ff0000")
		context.setLineWidth(2)
		context.moveTo(160, 100)
		context.arc(100, 100, 60, 0, 2 * Math.PI, true)
		context.moveTo(140, 100)
		context.arc(100, 100, 40, 0, Math.PI, false)
		context.moveTo(85, 80)
		context.arc(80, 80, 5, 0, 2 * Math.PI, true)
		context.moveTo(125, 80)
		context.arc(120, 80, 5, 0, 2 * Math.PI, true)
		context.stroke()
		context.draw()
	},
	methods: {
		canvasIdErrorCallback: function (e) {
			console.error(e.detail.errMsg)
		}
	}
}
```
 
相关 api：[uni.createCanvasContext](api/canvas/createCanvasContext)
Related api：[uni.createCanvasContext](api/canvas/createCanvasContext)

**扩展阅读**
**Extended reading**

canvas的常用用途有图表和图片处理，在uni-app插件市场有大量基于canvas的插件，可搜索 [图表](https://ext.dcloud.net.cn/search?q=图表) 、 [头像裁剪](https://ext.dcloud.net.cn/search?q=头像裁剪) 、 [海报](https://ext.dcloud.net.cn/search?q=海报) 、 [二维码](https://ext.dcloud.net.cn/search?q=%E4%BA%8C%E7%BB%B4%E7%A0%81) 。
canvas Common uses include charts and image processing, plug-in uni-app market has a large number of plug-in-based canvas, searchable [chart](https://ext.dcloud.net.cn/search?q=图表) , [picture cropping](https://ext.dcloud.net.cn/search?q=头像裁剪), [posters](https://ext.dcloud.net.cn/search?q=海报) , [two-dimensional code](https://ext.dcloud.net.cn/search?q=%E4%BA%8C%E7%BB%B4%E7%A0%81).

关于图表
About the chart
- H5端流行的echart报表因为涉及大量dom操作，无法跨端使用，而wx-chart在跨端和更新方面都不足。
- The popular echart report on the H5 end cannot be used cross-end because it involves a large number of dom operations, and wx-chart is insufficient in cross-end and update. If you are considering small programs, it is recommended to use uChart, which is available on all ends .
- 如只考虑H5端，也可以继续使用echart、f2等常规web图表。
- If you only consider the H5 end, you can continue to use regular web charts such as echart and f2.
- App端和H5，也可以通过renderjs技术来使用echart、f2等web图表，功能性能比uchart更好。[什么是renderjs](https://uniapp.dcloud.io/frame?id=renderjs)、[基于renderjs使用echart的示例](https://ext.dcloud.net.cn/plugin?id=1207)
- If you don't consider small programs, App and H5 can also use echart, f2 and other web charts through renderjs technology, which has better functional performance than uchart. [What is renderjs](https://uniapp.dcloud.io/frame?id=renderjs) , [an example of using echart based on renderjs](https://ext.dcloud.net.cn/plugin?id=1207)


**nvue页面如何使用canvas**
**How to use canvas on nvue page**

HBuilderX 2.2.5（alpha）开始 nvue 页面支持 Canvas，支持 W3C WebGL API [WebGL 1.0](https://www.khronos.org/registry/webgl/specs/latest/1.0/)
Starting from HBuilderX 2.2.5 (alpha), nvue pages support Canvas and W3C WebGL API [WebGL 1.0](https://www.khronos.org/registry/webgl/specs/latest/1.0/)

示例工程地址：[NvueCanvasDemo](https://github.com/dcloudio/NvueCanvasDemo)
Sample project address：[NvueCanvasDemo](https://github.com/dcloudio/NvueCanvasDemo)

在App端，从性能来讲，由于通讯阻塞的问题，nvue的canvas性能不可能达到使用renderjs的vue页面的canvas。在App端，推荐使用vue的canvas。
On the App side, in terms of performance, due to the problem of communication blocking, the canvas performance of nvue cannot reach the canvas of the vue page using renderjs. On the App side, Vue's canvas is recommended.