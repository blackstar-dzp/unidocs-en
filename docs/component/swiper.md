#### swiper

滑块视图容器。
Slider view container.

一般用于左右滑动或上下滑动，比如banner轮播图。
Generally used for sliding left and right or up and down, such as banner carousel.

注意滑动切换和滚动的区别，滑动切换是一屏一屏的切换。swiper下的每个swiper-item是一个滑动切换区域，不能停留在2个滑动区域之间。
Pay attention to the difference between sliding switch and scrolling, sliding switch is one screen one screen switch. Each swiper-item under swiper is a sliding switching area and cannot stay between 2 sliding areas.

**属性说明**
**Property description**

|属性名|类型|默认值|说明|平台差异说明|
| Attribute name| Types of    | Defaults| Description| Platform difference description |
|:-|:-|:-|:-|:-|
|indicator-dots|Boolean|false|是否显示面板指示点||
|indicator-dots|Boolean|false|Whether to display the panel indicator||
|indicator-color|Color|rgba(0, 0, 0, .3)|指示点颜色||
|indicator-color|Color|rgba(0, 0, 0, .3)|Point color||
|indicator-active-color|Color|#000000|当前选中的指示点颜色||
|indicator-active-color|Color|#000000|The currently selected indicator point color||
|autoplay|Boolean|false|是否自动切换||
|autoplay|Boolean|false|Whether to switch automatically||
|current|Number|0|当前所在滑块的 index||
|current|Number|0|The index of the current slider||
|current-item-id|String||当前所在滑块的 item-id ，不能与 current 被同时指定||
|current-item-id|String||The item-id of the current slider cannot be specified at the same time as current||
|interval|Number|5000|自动切换时间间隔||
|interval|Number|5000|Automatic switching time interval||
|duration|Number|500|滑动动画时长|app-nvue不支持|
|duration|Number|500|sliding animation duration|app-nvue does not support|
|duration|Number|500|Sliding animation duration|  app-nvue不支持|
|duration|Number|500|Sliding animation duration| not supported by app-nvue|
|circular|Boolean|false|是否采用衔接滑动，即播放到末尾后重新回到开头||
|circular|Boolean|false|Whether to use continuous sliding, that is, play back to the beginning after playing to the end||
|vertical|Boolean|false|滑动方向是否为纵向||
|vertical|Boolean|false|Whether the sliding direction is vertical||
|previous-margin|String|0px|前边距，可用于露出前一项的一小部分，接受 px 和 rpx 值|app-nvue|
|previous-margin|String|0px|Front margin, can be used to expose a small part of the previous item, accepts px and rpx values|app-nvue|
|next-margin|String|0px|后边距，可用于露出后一项的一小部分，接受 px 和 rpx 值|app-nvue|
|next-margin|String|0px|Back margin, can be used to expose a small part of the latter item, accept px and rpx values|app-nvue|
|display-multiple-items|Number|1|同时显示的滑块数量|app-nvue|
|display-multiple-items|Number|1|Number of sliders displayed at the same time|app-nvue|
|skip-hidden-item-layout|Boolean|false|是否跳过未显示的滑块布局，设为 true 可优化复杂情况下的滑动性能，但会丢失隐藏状态滑块的布局信息|App|
|skip-hidden-item-layout|Boolean|false|Whether to skip the unshown slider layout, set to true to optimize the sliding performance in complex situations, but the layout information of the hidden state slider will be lost|App|
|disable-touch|Boolean|false|是否禁止用户 touch 操作|App 2.5.5+、H5 2.5.5+|
|disable-touch|Boolean|false|Whether to prohibit user touch operation|App 2.5.5+、H5 2.5.5+|
|@change|EventHandle||current 改变时会触发 change 事件，event.detail = {current: current, source: source}||
|@change|EventHandle||The change event will be triggered when current changes, event.detail = {current: current, source: source}||
|@transition|EventHandle||swiper-item 的位置发生改变时会触发 transition 事件，event.detail = {dx: dx, dy: dy}，支付宝小程序暂不支持dx, dy|App、H5|
|@transition|EventHandle||The transition event will be triggered when the position of swiper-item changes, event.detail = {dx: dx, dy: dy}, Alipay applet does not support dx, dy|App、H5|
|@animationfinish|EventHandle||动画结束时会触发 animationfinish 事件，event.detail = {current: current, source: source}||
|@animationfinish|EventHandle||The animationfinish event will be triggered when the animation ends, event.detail = {current: current, source: source}||

change 事件返回 detail 中包含一个 source 字段，表示导致变更的原因，可能值如下：
The detail returned by the change event contains a source field, which indicates the cause of the change. The possible values are as follows:

- autoplay 自动播放导致swiper变化。
- autoplay autoplay causes swiper to change.
- touch 用户划动引起swiper变化。
- Touch user swipes to cause swiper changes.
- 其他原因将用空字符串表示。
- Other reasons will be indicated by an empty string.

**swiper做左右拖动的长列表的专项问题**
**Swiper does the special problem of dragging the long list left and right**
- swiper是单页组件，适合做banner图轮播和简单列表左右滑动。
- swiper is a single page component, suitable for banner image carousel and simple list sliding left and right.
- 因为性能问题，用swiper做复杂长列表，需要较高的优化技巧以及接受一些限制。
- Due to performance issues, using swiper to make complex and long lists requires high optimization skills and accepts some restrictions.
- 这是一个范例，[插件市场新闻模板示例](https://ext.dcloud.net.cn/plugin?id=103)，它在App端使用了nvue的原生渲染，实现高性能的左右拖动长列表；并支持可自定义的任何形式的下拉刷新。它在非App端使用的模式是只缓存左右一共3列的数据，dom中的数据过多时，它会自动释放。就是说App上，只要看过这一页，再进去时内容是还在的。而在非App上，只能做到缓存3页数据，其他页即便看过，再进去也会重新加载。并且非App的这种情况下，不再提供下拉刷新。虽然插件市场也有其他前端模拟的下拉刷新，但性能不佳。
- This is an example, [plugin market news template example](https://ext.dcloud.net.cn/plugin?id=103), which uses nvue's native rendering on the App side to achieve high-performance left and right drag Dynamic length list; and supports any form of customizable pull-down refresh. The mode it uses on the non-App side is to only cache the left and right columns of data. When there is too much data in the dom, it will be automatically released. That is to say, on the App, as long as you have read this page, the content will still be there when you enter it again. On non-Apps, only 3 pages of data can be cached, and other pages will be reloaded even if they are read. And in this case of non-App, pull-down refresh is no longer provided. Although the plug-in market also has other front-end analog pull-down refreshes, the performance is not good.
**Tips**

- 如果 nvue 页面 ``@animationfinish`` 事件不能返回正确的数据，可同时监听 ``@change`` 事件。
- If the ``@animationfinish`` event on the nvue page cannot return the correct data, you can monitor the ``@change`` event at the same time.
- 使用竖向滚动时，需要给 ``<scroll-view>`` 一个固定高度，通过 css 设置 height。
- -When using vertical scrolling, you need to give ``<scroll-view>`` a fixed height, and set the height through css.
- 注意：其中只可放置 ``<swiper-item>`` 组件，否则会导致未定义的行为。 
- Note: Only the ``<swiper-item>`` component can be placed in it, otherwise it will cause undefined behavior.
- 如果遇到current、current-item-id属性设置不生效的问题参考：[组件属性设置不生效解决办法](/vue-api?id=_4-组件属性设置不生效解决办法)
- If you encounter the problem that the current and current-item-id attribute settings do not take effect, please refer to: [Solution for component attribute settings not taking effect](/vue-api?id=_4-Solution for component attribute settings not taking effect)
- banner图的切换效果和指示器的样式，有多种风格可自定义，可在[uni-app插件市场](https://ext.dcloud.net.cn/search?q=%E8%BD%AE%E6%92%AD)搜索
- The switching effect of the banner image and the style of the indicator, there are a variety of styles that can be customized, which can be found in [uni-app plug-in market](https://ext.dcloud.net.cn/search?q=%E8%BD %AE%E6%92%AD) search
- 如需banner管理后台，参考uniCloud admin banner插件：[https://ext.dcloud.net.cn/plugin?id=4117](https://ext.dcloud.net.cn/plugin?id=4117)
- -For banner management background, refer to uniCloud admin banner plugin: [https://ext.dcloud.net.cn/plugin?id=4117](https://ext.dcloud.net.cn/plugin?id=4117 )
- swiper在App的vue中，不支持内嵌video、map等原生组件。在App nvue2.1.5起支持内嵌原生组件。竖向的swiper内嵌视频可实现抖音、映客等视频垂直拖动切换效果。
- swiper does not support native components such as embedded video and map in vue of App. From App nvue 2.1.5, it supports embedded native components. The vertical swiper embedded video can realize the vertical drag switching effect of Douyin, Inke and other videos.
- 同时监听 change transition，开始滑动时触发transition, 放开手后，在ios平台触发顺序为 transition... change，Android为 transition... change transition...
- Monitor the change transition at the same time, trigger the transition when you start sliding, and after letting go, the trigger sequence on the ios platform is transition... change, and Android is transition... change transition...
 
#### swiper-item
仅可放置在 ``<swiper>`` 组件中，宽高自动设置为100%。注意：宽高100%是相对于其父组件，不是相对于子组件，不能被子组件自动撑开。
It may be placed only in the `<swiper>`assembly, the width and height is automatically set to 100%. Note: 100% width and height are relative to the parent component, not to the child component, and cannot be automatically opened by the child component.
|属性名|类型|默认值|说明|
| Attribute name | Types of | Defaults | Description                       |
|:-|:-|:-|:-|:-|
|item-id|String||该 swiper-item 的标识符|
|item-id|String||The identifier of the swiper-item|

**示例** [查看演示](https://hellouniapp.dcloud.net.cn/pages/component/swiper/swiper)
**Example** [View Demo](https://hellouniapp.dcloud.net.cn/pages/component/swiper/swiper)

以下示例代码，来自于[hello uni-app项目](https://github.com/dcloudio/hello-uniapp)，推荐使用HBuilderX，新建uni-app项目，选择hello uni-app模板，可直接体验完整示例。
The following sample code comes from [hello uni-app project](https://github.com/dcloudio/hello-uniapp), it is recommended to use HBuilderX, create a new uni-app project, choose hello uni-app template, you can experience the complete Example.
```html
<!-- 本示例未包含完整css，获取外链css请参考上文，在hello uni-app项目中查看 -->
<template>
	<view>
		<view class="uni-padding-wrap">
			<view class="page-section swiper">
				<view class="page-section-spacing">
					<swiper class="swiper" :indicator-dots="indicatorDots" :autoplay="autoplay" :interval="interval" :duration="duration">
						<swiper-item>
							<view class="swiper-item uni-bg-red">A</view>
						</swiper-item>
						<swiper-item>
							<view class="swiper-item uni-bg-green">B</view>
						</swiper-item>
						<swiper-item>
							<view class="swiper-item uni-bg-blue">C</view>
						</swiper-item>
					</swiper>
				</view>
			</view>
		</view>
		<view class="swiper-list">
			<view class="uni-list-cell uni-list-cell-pd">
				<view class="uni-list-cell-db">Indicator point</view>
				<switch :checked="indicatorDots" @change="changeIndicatorDots" />
			</view>
			<view class="uni-list-cell uni-list-cell-pd">
				<view class="uni-list-cell-db">Autoplay</view>
				<switch :checked="autoplay" @change="changeAutoplay" />
			</view>
		</view>
		<view class="uni-padding-wrap">
			<view class="uni-common-mt">
				<text>Slideshow switching duration (ms)</text>
				<text class="info">{{duration}}</text>
			</view>
			<slider @change="durationChange" :value="duration" min="500" max="2000" />
			<view class="uni-common-mt">
				<text>Auto play interval time (ms)</text>
				<text class="info">{{interval}}</text>
			</view>
			<slider @change="intervalChange" :value="interval" min="2000" max="10000" />
		</view>
	</view>
</template>
```
```javascript
export default {
    data() {
        return {
            background: ['color1', 'color2', 'color3'],
            indicatorDots: true,
            autoplay: true,
            interval: 2000,
            duration: 500
        }
    },
    methods: {
        changeIndicatorDots(e) {
            this.indicatorDots = !this.indicatorDots
        },
        changeAutoplay(e) {
            this.autoplay = !this.autoplay
        },
        intervalChange(e) {
            this.interval = e.target.value
        },
        durationChange(e) {
            this.duration = e.target.value
        }
    }
}
```
 ![uni](https://bjetxgzv.cdn.bspapp.com/VKCEYUGU-uni-app-doc/97ccca10-4f2f-11eb-b997-9918a5dda011.png)
