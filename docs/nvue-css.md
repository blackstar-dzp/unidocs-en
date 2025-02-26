
#### nvue所支持的通用样式已在本文档中全部列出，一些组件可能有自定义样式，请参考组件文档。除此之外的属性，均不被支持。
#### The general styles supported by nvue are all listed in this document. Some components may have custom styles, please refer to the component documentation. Other attributes are not supported.

### 注意事项
### Precautions

- nvue的css**仅支持flex布局**，是webview的css语法的子集。这是因为操作系统原生排版不支持非flex之外的web布局。当然flex足以排布出各种页面，只是写法需要适应。
- nvue's css** only supports flex layout**, which is a subset of webview's css syntax. This is because the native typesetting of the operating system does not support web layouts other than non-flex. Of course, flex is enough to arrange various pages, but the writing needs to be adapted.
- class 进行绑定时只支持数组语法。
- Class only supports array syntax when binding.
- 不支持媒体查询
- Media queries are not supported
- 不能在 style 中引入字体文件
- Cannot include font files in style
- 不能使用百分比布局，如`width：100%`
- Cannot use percentage layout, such as `width: 100%`
- 不支持在css里写背景图`background-image`，但可以使用image组件和层级来实现类似web中的背景效果。因为原生开发本身也没有web这种背景图概念
- It does not support writing background image `background-image` in css, but image components and layers can be used to achieve background effects similar to those in the web. Because native development itself does not have the concept of web background images
- 使用`image`标签，支持使用base64
- Use the `image` tag, support the use of base64
- nvue 的各组件在安卓端默认是透明的，如果不设置`background-color`，可能会导致出现重影的问题
- Each component of nvue is transparent by default on the Android side. If you do not set the `background-color`, it may cause ghosting problems
- 文字内容，必须只能在`text`组件下，`text`组件不能换行写内容，否则会出现无法去除的周边空白
- The text content must only be under the `text` component, and the `text` component cannot write content in a new line, otherwise there will be surrounding blanks that cannot be removed
- 只有`text`标签可以设置字体大小，字体颜色
- Only the `text` tag can set the font size and font color


**HBuilderX 3.1.0+ 开始支持更多简写样式**
**HBuilderX 3.1.0+ starts to support more abbreviated styles**
- `border`
- `border-top`
- `border-right`
- `border-bottom`
- `border-left`
- `border-style`
- `border-width`
- `border-color`
- `border-radius`
- `flex-flow`
- `background`


**HBuilderX 3.1.0+ 开始支持新的样式编译模式**
**HBuilderX 3.1.0+ starts to support the new style compilation mode**

- 新增 `nvueStyleCompiler` 配置，支持组合选择器（相邻兄弟选择器、普通兄弟选择器、子选择器、后代选择器）。[详见](https://ask.dcloud.net.cn/article/38751)
- Added `nvueStyleCompiler` configuration to support combined selectors (adjacent brother selector, normal brother selector, child selector, descendant selector). [See details](https://ask.dcloud.net.cn/article/38751)

- nvue的```uni-app```编译模式下，App.vue 中的样式，会编译到每个 nvue文件。对于共享样式，如果有不合法属性控制台会给出警告，可以通过[条件编译](https://uniapp.dcloud.io/platform)```APP-PLUS-NVUE```屏蔽 App 中的警告。
- Under nvue's ``uni-app``` compilation mode, the styles in App.vue will be compiled to each nvue file. For shared styles, if there are illegal attributes, the console will give a warning. You can use [Conditional Compilation](https://uniapp.dcloud.io/platform)```APP-PLUS-NVUE``` to block the App warn.

## 盒模型
## Box model

nvue盒模型基于 CSS 盒模型，每个 nvue 元素都可视作一个盒子。我们一般在讨论设计或布局时，会提到「盒模型」这个概念。
The nvue box model is based on the CSS box model, and each nvue element can be regarded as a box. We generally mention the concept of "box model" when discussing design or layout.

盒模型描述了一个元素所占用的空间。每一个盒子有四条边界：外边距边界 `margin edge`, 边框边界 `border edge`, 内边距边界 `padding edge` 与内容边界 `content edge`。这四层边界，形成一层层的盒子包裹起来，这就是盒模型大体上的含义。
The box model describes the space occupied by an element. Each box has four borders: margin edge `margin edge`, border border `border edge`, inner margin border `padding edge` and content border `content edge`. These four layers of boundaries form a layer of boxes wrapped up, which is the general meaning of the box model.

![图片描述文字](https://bjetxgzv.cdn.bspapp.com/VKCEYUGU-dc-site/ec4f2810-2fec-11eb-899d-733ae62bed2f.png)
![Picture description text](https://bjetxgzv.cdn.bspapp.com/VKCEYUGU-dc-site/ec4f2810-2fec-11eb-899d-733ae62bed2f.png)

> nvue盒模型的 `box-sizing` 默认为 `border-box`，即盒子的宽高包含内容、内边距和边框的宽度，不包含外边距的宽度。
> The `box-sizing` of the nvue box model defaults to `border-box`, that is, the width and height of the box include the width of the content, inner margin and border, but not the width of the outer margin.

> 在 Android 平台，nvue只支持 `overflow:hidden`。
> On the Android platform, nvue only supports `overflow:hidden`.

> 在 iOS 上，nvue支持 `overflow:hidden` 和 `overflow:visible`，默认是 `overflow:visible`。
> On iOS, nvue supports `overflow:hidden` and `overflow:visible`, and the default is `overflow:visible`.


##### 基本用法
##### Basic usage
```html
	<template>
		<view>
			<image style="width: 400rpx; height: 200rpx; margin-left: 20rpx;" src="https://bjetxgzv.cdn.bspapp.com/VKCEYUGU-dc-site/9c877c50-2f0c-11eb-899d-733ae62bed2f.png"></image>
		</view>
	</template>
```



|可选值			|描述									|
|Optional value |Description |
|--				|--										|
|width {length}	|宽度，默认值 0							|
|width {length} |width, default value 0 |
|height {length}|高度，默认值 0							|
|height {length}|Height, default value 0 |

##### 内边距
##### Inner Margin
padding {length}：内边距，内容和边框之间的距离，默认值 0。与标准 CSS 类似，padding 支持简写，也可分解为以下四个：
padding {length}: padding, the distance between the content and the border, the default value is 0. Similar to standard CSS, padding supports abbreviations, which can also be broken down into the following four:
|可选值					|描述								|
|Optional value |Description |
|--						|--									|
|padding {length}		|上、右、下、左四边内边距，默认值 0	|
|padding {length} |The padding of the top, right, bottom, and left sides, the default value is 0 |
|padding-left {length}	|左内边距，默认值 0					|
|padding-left {length} |Left padding, default value 0 |
|padding-right {length}	|右内边距，默认值 0					|
|padding-right {length} |Right padding, default value 0 |
|padding-top {length}	|上内边距，默认值 0					|
|padding-top {length} |Top padding, default value 0 |
|padding-bottom {length}|下内边距，默认值 0					|
|padding-bottom {length}|Bottom padding, default value 0 |

##### 边框
##### Border
```border-style``` 设定边框样式，如果四个方向的边框样式不同，可分别设置：
```border-style``` Set the border style. If the border styles in the four directions are different, you can set them separately:
|可选值	|描述					|
|Optional value |Description |
|--		|--						|
|border-left-style {string}		|可选值为 ```solid```， ```dashed```， ```dotted```，默认值 ```solid```	|
|border-left-style {string} |The optional values are ```solid```, ```dashed```, ```dotted```, the default value is ```solid``` |
|border-top-style {string}		|可选值为 ```solid```， ```dashed```， ```dotted```，默认值 ```solid```	|
|border-top-style {string} |The optional values are ```solid```, ```dashed```, ```dotted```, the default value is ```solid``` |
|border-right-style {string}	|可选值为 ```solid```， ```dashed```， ```dotted```，默认值 ```solid```	|
|border-right-style {string} |The optional values are ```solid```, ```dashed```, ```dotted```, the default value is ```solid``` |
|border-bottom-style {string}	|可选值为 ```solid```， ```dashed```， ```dotted```，默认值 ```solid```	|
|border-bottom-style {string} |The optional values are ```solid```, ```dashed```, ```dotted```, the default value is ```solid``` |


|可选值	|描述					|
|Optional value |Description |
|--		|--						|
|solid	|实线边框，默认值 ```solid```	|
|solid |Solid border, default value ```solid``` |
|dashed	|方形虚线边框			|
|dashed |Square dotted border |
|dotted	|圆点虚线边框			|
|dotted |Dotted dotted border |

##### border-width
```border-width```：设定边框宽度，非负值, 默认值 0，如果四个方向的边框宽度不同，可分别设置：
```border-width```: Set the border width, non-negative value, default value 0, if the border widths in the four directions are different, you can set them separately:

|可选值							|描述				|
|Optional value |Description |
|--								|--					|
|border-width {length}			|非负值, 默认值 0	|
|border-width {length} |Non-negative value, default value 0 |
|border-left-width {length}		|非负值, 默认值 0	|
|border-left-width {length} |Non-negative value, default value 0 |
|border-top-width {length}		|非负值, 默认值 0	|
|border-top-width {length} |Non-negative value, default value 0 |
|border-right-width {length}	|非负值, 默认值 0	|
|border-right-width {length} |Non-negative value, default value 0 |
|border-bottom-width {length}	|非负值, 默认值 0	|
|border-bottom-width {length} |Non-negative value, default value 0 |

##### border-color
```border-color```：设定边框颜色，默认值 ```#000000```，如果四个方向的边框颜色不同，可分别设置：
```border-color```: Set the border color, the default value is ```#000000```, if the border colors in the four directions are different, you can set them separately:

|可选值						|描述					|
|Optional value |Description |
|--							|--						|
|border-color {color}		|默认值 ```#000000```	|
|border-color (color) |default value ```#000000``` |
|border-left-color {color}	|默认值 ```#000000```	|
|border-left-color (color) |default value ```#000000``` |
|border-top-color {color}	|默认值 ```#000000```	|
|border-top-color (color) |default value ```#000000``` |
|border-right-color {color}	|默认值 ```#000000```	|
|border-right-color (color) |default value ```#000000``` |
|border-bottom-color {color}|默认值 ```#000000```	|
|border-bottom-color (color)|default value ```#000000``` |


##### border-radius
```border-radius```：设置边框的圆角，默认值 0，如果四个方向的圆角弧度不同，可分别设置：
```border-radius```: Set the rounded corners of the border, the default value is 0, if the rounded corners in the four directions are different, you can set them separately:
|可选值								|描述				|
|Optional value |Description |
|--									|--					|
|border-radius {length}				|非负值, 默认值 0	|
|border-radius {length} |Non-negative value, default value 0 |
|border-bottom-left-radius {length}	|非负值, 默认值 0	|
|border-bottom-left-radius {length} |Non-negative value, default value 0 |
|border-bottom-right-radius {length}|非负值, 默认值 0	|
|border-bottom-right-radius {length}|Non-negative value, default value 0 |
|border-top-left-radius {length}	|非负值, 默认值 0	|
|border-top-left-radius {length} |Non-negative value, default value 0 |
|border-top-right-radius {length}	|非负值, 默认值 0	|
|border-top-right-radius {length} |Non-negative value, default value 0 |
> ```border-radius```和```border-width```定义了圆心角为90度的椭圆弧的长轴和半长轴的大小。如果邻接两边```border-radius```(或```border-width```不一致，nvue绘制的边框曲线可能不够平滑。
> ```border-radius``` and ```border-width``` define the size of the major axis and the semi-major axis of an elliptical arc with a central angle of 90 degrees. If the adjacent sides of ```border-radius``` (or ```border-width``` are inconsistent, the border curve drawn by nvue may not be smooth enough.


##### 外边距
##### Margin
margin {length}：外边距，元素和元素之间的空白距离，默认值 0。与标准 CSS 类似，margin 支持简写，也可分解为四边：
margin {length}: The margin, the blank distance between the element and the element, the default value is 0. Similar to standard CSS, margin supports abbreviation and can also be decomposed into four sides:

|可选值					|描述								|
|Optional value |Description |
|--						|--									|
|margin {length}		|上、右、下、左四边外边距，默认值 0	|
|margin {length} |The top, right, bottom and left margins, the default value is 0 |
|margin-left {length}	|左外边距，默认值 0					|
|margin-left {length} |Left margin, default value 0 |
|margin-right {length}	|右外边距，默认值 0					|
|margin-right {length} |Right margin, default value 0 |
|margin-top {length}	|上外边距，默认值 0					|
|margin-top {length} |Top margin, default value 0 |
|margin-bottom {length}	|下外边距，默认值 0					|
|margin-bottom {length} |Bottom margin, default value 0 |


##### Android 兼容性
##### Android compatibility
尽管 ```overflow: hidden``` 在 Android 上是默认行为，但只有下列条件都满足时，一个父 view 才会去剪切它的子 ```view```。
Although ```overflow: hidden``` is the default behavior on Android, only when the following conditions are met, a parent view will cut its child ```view```.
- 父view是```view```, ```cell```, ```refresh``` 或 ```loading```。
- The parent view is ```view```, ```cell```, ```refresh``` or ```loading```.
- 系统版本是 Android 4.3 或更高。
- The system version is Android 4.3 or higher.
- 系统版本不是 Andorid 7.0。
- The system version is not Andorid 7.0.
- 父 view 没有 ```background-image``` 属性或系统版本是 Android 5.0 或更高。
- The parent view does not have the ```background-image``` attribute or the system version is Android 5.0 or higher.


### Flex 容器
### Flexbox

Flex 是 Flexible Box 的缩写，意为"弹性布局"，用来为盒状模型提供最大的灵活性。
Flex is the abbreviation of Flexible Box, which means "flexible layout" and is used to provide maximum flexibility for box models.

nvue布局模型基于 CSS Flexbox，以便所有页面元素的排版能够一致可预测，同时页面布局能适应各种设备或者屏幕尺寸。Flexbox 包含 flex 容器和 flex 成员项。如果一个nvue元素可以容纳其他元素，那么它就成为 flex 容器。
The nvue layout model is based on CSS Flexbox, so that the layout of all page elements can be consistent and predictable, and the page layout can adapt to various devices or screen sizes. Flexbox contains flex container and flex member items. If an nvue element can hold other elements, then it becomes a flex container.
> 文档中未说明的 flexbox 属性**均不支持**：如 ```order```、```flex-grow``` 、```flex-shrink``` 、 ```flex-basis```、```align-content```、```align-self``` 等。
> The flexbox properties that are not explained in the document ** are not supported**: such as ```order```, ```flex-grow```, ```flex-shrink```, ```flex- basis```, ```align-content```, ```align-self``` etc.
**在 nvue中，Flexbox 是默认且唯一的布局模型，所以你不需要手动为元素添加 ```display: flex;``` 属性。**
**In nvue, Flexbox is the default and only layout model, so you don't need to manually add the ```display: flex;``` attribute to the element.**

### flex-direction
	
定义了 flex 容器中 flex 成员项的排列方向，默认值为 ```column```
Defines the arrangement direction of the flex member items in the flex container, the default value is ```column```
|可选值			|描述								|
|Optional value |Description |
|--				|--									|
|column			|竖排，从上到下排列					|
|column |Vertical, arranged from top to bottom |
|column-reverse	|反向竖排，排布方向与```flex-direction:column```相反|
|column-reverse |Reverse vertical arrangement, the arrangement direction is opposite to ```flex-direction:column```|
|row			|横排，从左到右排布						|
|row |Horizontal, from left to right |
|row-reverse	|反向横排，排布方向与```flex-direction:row```相反	|
|row-reverse |Reverse horizontal arrangement, the arrangement direction is opposite to ```flex-direction:row``` |

### flex-wrap
	
决定了 flex 成员项在一行还是多行分布，默认值为```nowrap```
Determines whether the flex member items are distributed in one line or multiple lines. The default value is ```nowrap```
|可选值			|描述												|
|Optional value |Description |
|--				|--													|
|nowrap			| 不换行，flex 成员项在一行排布，排布的开始位置由direction指定	|
|nowrap | No line break, flex member items are arranged in one line, and the starting position of the arrangement is specified by direction |
|wrap			| 换行，第一行在上方，flex 成员项在多行排布，排布的开始位置由direction指定	|
|wrap | Wrap, the first line is at the top, the flex member items are arranged in multiple lines, and the starting position of the arrangement is specified by direction |
|wrap-reverse	|换行，第一行在下方，行为类似于```wrap```，排布方向与其相反						|
|wrap-reverse | Wrap, the first line is below, the behavior is similar to ```wrap```, the arrangement direction is opposite to it |

### justify-content
	
定义了 flex 容器中 flex 成员项在主轴方向上如何排列以处理空白部分。默认值为 ```flex-start```
Defines how the flex member items in the flex container are arranged in the main axis direction to deal with the blank part. The default value is ```flex-start```


|可选值			|描述										|
|Optional value |Description |
|--				|--											|
|flex-start		|左对齐，所有的 flex 成员项都排列在容器的前部	|
|flex-start |Left aligned, all flex member items are arranged at the front of the container |
|flex-end		|右对齐，则意味着成员项排列在容器的后部			|
|flex-end |Right-aligned, it means that the member items are arranged at the back of the container |
|center			|居中，即中间对齐，成员项排列在容器中间、两边留白		|
|center |Centered, that is, aligned in the middle, the member items are arranged in the middle of the container, with blanks on both sides |
|space-between	|两端对齐，空白均匀地填充到 flex 成员项之间	|
|space-between |Justified at both ends, the blanks are evenly filled between the flex member items |
|space-around	|表示 flex 成员项两侧的间隔相等，所以，成员项之间的间隔比成员项与边框的间隔大一倍	|
|space-around | Means that the intervals on both sides of the flex member items are equal, so the interval between the member items is twice as large as the interval between the member items and the border |

![图片描述文字](https://bjetxgzv.cdn.bspapp.com/VKCEYUGU-dc-site/9610d190-2f17-11eb-97b7-0dc4655d6e68.png)
![Picture description text](https://bjetxgzv.cdn.bspapp.com/VKCEYUGU-dc-site/9610d190-2f17-11eb-97b7-0dc4655d6e68.png)
	
### align-items
	
定义了 flex 容器中 flex 成员项在纵轴方向上如何排列以处理空白部分。默认值为 stretch。
Defines how the flex member items in the flex container are arranged along the vertical axis to deal with the blank part. The default value is stretch.

|可选值		|描述								|
|Optional value |Description |
|--			|--									|
|stretch	|即拉伸高度至 flex 容器的大小			|
|stretch |That is to stretch the height to the size of the flex container |
|flex-start	|上对齐，所有的成员项排列在容器顶部	|
|flex-start |Top alignment, all member items are arranged at the top of the container |
|flex-end	|下对齐，所有的成员项排列在容器底部	|
|flex-end | Align bottom, all member items are arranged at the bottom of the container |
|center		|中间对齐，所有成员项都垂直地居中显示	|
|center |Aligned in the middle, all member items are displayed vertically in the center |
![图片描述文字](https://bjetxgzv.cdn.bspapp.com/VKCEYUGU-dc-site/ad305030-2f17-11eb-b680-7980c8a877b8.png)
![Picture description text](https://bjetxgzv.cdn.bspapp.com/VKCEYUGU-dc-site/ad305030-2f17-11eb-b680-7980c8a877b8.png)


### flex
	
flex 属性定义了 flex 成员项可以占用容器中剩余空间的大小。
The flex attribute defines how much flex member items can occupy the remaining space in the container.

flex {number}：值为 number 类型。
flex {number}: The value is of type number.

- 如果所有的成员项设置相同的值 flex: 1，它们将平均分配剩余空间。
- If all member items are set to the same value flex: 1, they will equally distribute the remaining space.

- 经常用作自适应布局，将父容器的display：flex，侧边栏大小固定后，将内容区flex：1，内容区则会自动放大占满剩余空间。
- It is often used as an adaptive layout. After fixing the display: flex of the parent container and the size of the sidebar, set the content area to flex:1, and the content area will be automatically enlarged to take up the remaining space.

- 如果一个成员项设置的值为 flex: 2，其它的成员项设置的值为 flex: 1，那么这个成员项所占用的剩余空间是其它成员项的 2 倍。
- If a member item is set to flex: 2 and other member items are set to flex: 1, then the remaining space occupied by this member item is twice that of other member items.

**注意**
**Notice**

**Flex 成员项暂不支持 ```flex-shrink``` 、 ```flex-basis```、```align-content``` 属性**。
**Flex member items do not currently support ```flex-shrink```, ```flex-basis```, ```align-content``` properties**.

**该属性不支持 flex: flex-grow | flex-shrink | flex-basis 的简写。**
**This property does not support the abbreviation of flex: flex-grow | flex-shrink | flex-basis.**

``` html
	//Gird布局
	//Gird layout
	<template>
		<view>
			<view v-for="(v, i) in list" class="row">
				<view v-for="(text, k) in v" class="item">
					<view>
						<text>{{text}}</text>
					</view>
				</view>
			</view>
		</view>
	</template>
	<script>
		export default {
			data() {
				return {
					list: [
						['A', 'B', 'C'],
						['D', 'E', 'F'],
						['G', 'H', 'I']
					]
				}
			}
		}
	</script>
	<style scoped>
	.row {
		flex-direction: row;
		height: 80px;
	}
	.item {
		flex: 1;
		justify-content: center;
		align-items: center;
		border-width: 1;
		border-style: solid;
		border-color: #FFFFFF;
		background-color: #00AAFF;
	}
	</style>
```



``` html
	//等高模块
	//Contour module
	<template>
	  <view>
	    <view style="width:300px; height:100px;">
	      <view style="flex: 1;background-color:blue"></view>
	      <view style="flex: 1;background-color:red"></view>
	      <view style="flex: 1;background-color:yellow"></view>
	    </view>
	  </view>
	</template>
```




## position 定位
## position

设置定位类型。默认值为 ```relative```。
Set the targeting type. The default value is ```relative```.


|可选值		|描述													|
|Optional value |Description |
|--			|--														|
|relative	|是默认值，指的是相对定位									|
|relative | is the default value, refers to relative positioning |
|absolute	|绝对定位，以元素的容器作为参考系						|
|absolute |Absolute positioning, with the container of the element as the reference system |
|fixed		|固定定位，保证元素在页面窗口中的对应位置显示，即使窗口是滚动的它也不会移动						|
|fixed |Fixed positioning, to ensure that the element is displayed in the corresponding position in the page window, even if the window is scrolling, it will not move |
|sticky		|指的是仅当元素滚动到页面之外时，元素会固定在页面窗口的顶部，达到吸顶效果/粘性定位（布局）	|
|sticky | means that only when the element is scrolled outside the page, the element will be fixed at the top of the page window to achieve a ceiling effect/sticky positioning (layout) |

> 运用 position:sticky或position: fixed 可实现头部导航栏固定(吸顶效果)
> Use position:sticky or position: fixed to achieve a fixed head navigation bar (ceiling effect)

``` html
	//水平垂直居中
	//Center horizontally and vertically
	<template>
		<view class="wrapper">
			<view class="box"></view>
		</view>
	</template>
	<style scoped>
		.wrapper{
			position: absolute;
			top: 0;
			right: 0;
			bottom: 0;
			left: 0;
			background-color: #cccccc;
			justify-content: center;
			align-items: center;
		}
		.box{
			width: 200px;
			height: 200px;
			background-color: #fc0000;
		}
	</style>
```


> Android 兼容性
> Android compatibility
如果定位元素超过容器边界，在 Android 下，超出部分将不可见，原因在于 Android 端元素 ```overflow``` 默认值为 ```hidden```，但目前 Android 暂不支持设置 ```overflow: visible```。
If the positioning element exceeds the container boundary, under Android, the excess part will not be visible. The reason is that the default value of the Android element ```overflow``` is ```hidden```, but currently Android does not support setting ``` overflow: visible```.

## Transition 

```transition```允许 CSS 的属性值在一定的时间区间内平滑地过渡。
```transition``` allows CSS property values to transition smoothly within a certain time interval.
#### transition-property
设置过渡动画的属性名，设置不同样式 ```transition``` 效果的键值对，默认值为空，表示不执行任何过渡效果
Set the attribute name of the transition animation, set the key-value pairs of different styles of ```transition``` effect, the default value is empty, which means that no transition effect will be performed

|参数名				|描述				|
|Parameter name |Description |
|--					|--					|
|width				|宽度参与过渡动画		|
|width |Width participates in transition animation |
|height				|高度参与过渡动画		|
|height |Height participation in transition animation |
|top				|顶部距离参与过渡动画	|
|top |Top distance participates in transition animation |
|bottom				|底部距离参与过渡动画	|
|bottom |The bottom distance participates in the transition animation |
|left				|左侧距离参与过渡动画	|
|left |The left distance participates in the transition animation |
|right				|右侧距离参与过渡动画	|
|right |The distance on the right is involved in the transition animation |
|background-color	|背景颜色参与过渡动画	|
|background-color |The background color participates in the transition animation |
|opacity			|不透明度参与过渡动画	|
|opacity |Opacity participates in transition animation |
|transform			|变换类型参与过渡动画	|
|transform |Transformation type participates in transition animation |


#### transition-duration
指定过渡的持续时间 (单位是毫秒)，默认值是 0，表示没有动画效果。
Specify the duration of the transition (in milliseconds), the default value is 0, which means there is no animation effect.
#### transition-delay
指定请求过渡操作到执行过渡之间的时间间隔 (单位是毫秒或者秒)，默认值是 0，表示没有延迟，在请求后立即执行过渡。
Specify the time interval (in milliseconds or seconds) between requesting a transition operation and executing the transition. The default value is 0, which means there is no delay, and the transition will be executed immediately after the request.
#### transition-timing-function
描述过渡执行的速度曲线，用于使过渡更为平滑。默认值是 ```ease```。下表列出了所有合法的属性：
Describe the speed curve of the transition execution, used to make the transition smoother. The default value is ```ease```. The following table lists all legal attributes:

|参数名							|描述																																			|
|Parameter name |Description |
|--								|--																																				|
|ease							|transition 过渡逐渐变慢的过渡效果																												|
|ease |transition The transition effect that gradually slows down the transition |
|ease-in						|transition 过渡慢速开始，然后变快的过渡效果																									|
|ease-in |transition Transition effect that starts slowly and then becomes faster |
|ease-out						|transition 过渡快速开始，然后变慢的过渡效果																									|
|ease-out |transition Transition that starts quickly and then slows down |
|ease-in-out					|transition 过渡慢速开始，然后变快，然后慢速结束的过渡效果																						|
|ease-in-out |transition The transition effect that the transition starts slowly, then becomes faster, and then ends slowly |
|linear							|transition 过渡以匀速变化																														|
|linear |transition Transition changes at a constant speed |
|cubic-bezier(x1, y1, x2, y2)	|使用三阶贝塞尔函数中自定义 transition 变化过程，函数的参数值必须处于 0 到 1 之间。更多关于三次贝塞尔的信息请参阅  [cubic-bezier](https://cubic-bezier.com/?spm=a2c7j.-zh-docs-styles-common-styles.0.0.3f952164z39lZD#.17,.67,.83,.67)和 [Bézier curve](https://en.wikipedia.org/wiki/B%C3%A9zier_curve?spm=a2c7j.-zh-docs-styles-common-styles.0.0.3f952164z39lZD)	|
|cubic-bezier(x1, y1, x2, y2) |Using the custom transition process in the third-order Bezier function, the parameter value of the function must be between 0 and 1. For more information about Cubic Bezier, please refer to [cubic-bezier](https://cubic-bezier.com/?spm=a2c7j.-zh-docs-styles-common-styles.0.0.3f952164z39lZD#.17, .67, .83, .67) and [Bézier curve](https://en.wikipedia.org/wiki/B%C3%A9zier_curve?spm=a2c7j.-zh-docs-styles-common-styles.0.0. 3f952164z39lZD) |
	
#### 示例
#### Example

``` html
<template>
	<view class="row">
		<view class="box" :class="{'active':isActive}" @click="isActive = !isActive">
			<image class="img" src="https://bjetxgzv.cdn.bspapp.com/VKCEYUGU-dc-site/9c877c50-2f0c-11eb-899d-733ae62bed2f.png" mode="aspectFill"></image>
		</view>
	</view>
</template>
<script>
	export default {
		data() {
			return {
				"isActive":false
			}
		}
	}
</script>
<style scoped>
	.row{
		align-items: center;
		justify-content: center;
	}
	.box{
		margin:20px;
		align-items: center;
		justify-content: center;
		border-radius: 10px;
		width:200rpx;
		height:200rpx;
		background-color: #007AFF;
		transition-property: width, height, background-color;
		transition-duration:0.3s;
		transition-delay:0.1s;
		transition-timing-function: cubic-bezier(0.25, 0.1, 0.25, 1.0);
	}
	.active{
		width:300rpx;
		height:300rpx;
		background-color: #6bd8ff;
	}
	.img{
		width:80rpx;
		height:80rpx;
	}
</style>
```

<img width="300px" src="https://bjetxgzv.cdn.bspapp.com/VKCEYUGU-dc-site/0d2fc7a0-3089-11eb-8ff1-d5dcf8779628.gif" />

## Transform

应用于元素的2D或3D转换。这个属性允许你将元素旋转，缩放，移动，倾斜等。
2D or 3D transformation applied to the element. This property allows you to rotate, scale, move, tilt, etc. the element.

|参数名							|描述																																			|
|Parameter name |Description |
|--								|--																																				|
|`translateX({<length/percentage>})`	|X 轴方向平移，支持长度单位或百分比。																												|
|`translateX({<length/percentage>})` |X-axis translation, support length unit or percentage. |
|`translateY({<length/percentage>})`	|Y 轴方向平移，支持长度单位或百分比。																	|
|`translateY({<length/percentage>})` |Y-axis translation, support length unit or percentage. |
|`translate({<length/percentage>} {<length/percentage>})`	|X 轴和 Y 轴方向同时平移，```translateX``` + ```translateY``` 简写。									|
|`translate({<length/percentage>} {<length/percentage>})` | Simultaneous translation in X and Y directions, shorthand for ```translateX``` + ```translateY```. |
|`scaleX(<number>)`				|X 轴方向缩放，值为数值，表示缩放比例，不支持百分比。							|
|`scaleX(<number>)` |X-axis zoom, the value is a numeric value, indicating the zoom ratio, and percentages are not supported. |
|`scaleY(<number>)`						|Y 轴方向缩放，值为数值，表示缩放比例，不支持百分比。																													|
|`scaleY(<number>)` |Zoom in the Y-axis direction. The value is a numeric value, indicating the zoom ratio. Percentage is not supported. |
|`scale(<number>)`|X 轴和 Y 轴方向同时缩放，```scaleX``` + ```scaleY``` 简写。|
|`scale(<number>)`|X-axis and Y-axis directions are zoomed at the same time, ```scaleX``` + ```scaleY``` abbreviation. |
|`rotate(<angle/degree>)`|将元素围绕一个定点（由 ```transform-origin``` 属性指定）旋转而不变形的转换。指定的角度定义了旋转的量度。若角度为正，则顺时针方向旋转，否则逆时针方向旋转。|
|`rotate(<angle/degree>)`|Transformation that rotates the element around a fixed point (specified by the ```transform-origin``` attribute) without deformation. The specified angle defines the measure of rotation. If the angle is positive, it rotates clockwise, otherwise it rotates counterclockwise. |
|`rotateX(<angle/degree>)`|X 轴方向的旋转。|
|`rotateX(<angle/degree>)`|Rotation in the X axis direction. |
|`rotateY(<angle/degree>)`|Y 轴方向的旋转。|
|`rotateY(<angle/degree>)`|Rotation in Y axis direction. |
|`rotateZ(<angle/degree>)`|Z 轴方向的旋转。|
|`rotateZ(<angle/degree>)`|The rotation in the Z axis direction. |
|`perspective(<length>)`|指定了观察者与 z=0 平面的距离，使具有三维位置变换的元素产生透视效果。z>0 的三维元素比正常大，而 z<0 时则比正常小，大小程度由该属性的值决定。Android 4.1及以上版本支持。|
|`perspective(<length>)`| specifies the distance between the observer and the z=0 plane, so that the element with three-dimensional position transformation produces a perspective effect. The three-dimensional element with z>0 is larger than normal, and when z<0, it is smaller than normal. The size is determined by the value of this attribute. Support for Android 4.1 and above. |
|`transform-origin {length/percentage/关键字(top/left/right/bottom)}:`|设置一个元素变形的原点，仅支持 2D 坐标。|
|`transform-origin {length/percentage/keyword (top/left/right/bottom)}:`|Set the origin of an element's transformation, only 2D coordinates are supported. |

> 除了```perspective```和```transform-origin```，```transition```支持了```transform```的全部能力。 其中transform的```rotate``` 和```rotatez``` 等效.
> Except for ```perspective``` and ```transform-origin```, ```transition``` supports all the capabilities of ```transform```. Among them, ```rotate``` of transform is equivalent to ```rotatez```.
	
#### 示例
#### Example

``` html
<template>
	<view class="card">
		<view class="box">
			<view class="row-box">
				<view @click="isRotate = !isRotate" class="fill row-rotate " :class="{'rotate':isRotate}"></view>
			</view>
			<text>rotate(45deg) </text>
		</view>
		<view class="box">
			<view class="row-box">
				<view @click="isScale = !isScale" class="fill row-scale" :class="{'scale':isScale}"></view>
			</view>
			<text>scale(2)</text>
		</view>
		<view class="box">
			<view class="row-box">
				<view @click="isTranslateX = !isTranslateX" class="fill row-translateX" :class="{'translateX':isTranslateX}"></view>
			</view>
			<text>translateX(45px)</text>
		</view>
		<view class="box">
			<view class="row-box">
				<view @click="isTranslateY = !isTranslateY" class="fill row-translateY" :class="{'translateY':isTranslateY}"></view>
			</view>
			<text>translateY(45px)</text>
		</view>
	</view>
</template>
<script>
	export default {
		data() {
			return {
				"isRotate": false,
				"isScale":false,
				"isTranslateX":false,
				"isTranslateY":false
			}
		},
	}
</script>
<style>
	.card {
		width:710rpx;
		margin:20rpx;
		flex-direction:row;
		flex-wrap: wrap;
	}
	.box{
		width:355rpx;
		height:355rpx;
		justify-content: center;
		align-items: center;
	}
	.row-box{
		width:200rpx;
		height:200rpx;
		margin:10rpx;
		background-color: #DDDDDD;
	}
	.fill{
		width:200rpx;
		height:200rpx;
		position: relative;
		background-color: #03A9F4;
		opacity: 0.5;
	}
	.row-rotate{
		transition-duration:0.3s;
		transform:rotate(0deg);
	}
	.rotate{
		transition-duration:0.3s;
		transform:rotate(45deg);
	}
	.row-scale{
		transition-duration:0.3s;
		transform:scale(1);
	}
	.scale{
		transform:scale(2);
	}
	.row-translateX{
		transition-duration:0.3s;
		transform:translateX(0px);
	}
	.translateX{
		transform:translateX(45px);
	}
	.row-translateY{
		transition-duration:0.3s;
		transform:translateY(0px);
	}
	.translateY{
		transform:translateY(45px);
	}
</style>
```





<img width="300px" src="https://bjetxgzv.cdn.bspapp.com/VKCEYUGU-dc-site/810e5de0-3088-11eb-b997-9918a5dda011.gif" />


## 伪类
## Pseudo-class

|参数名		|描述								|
|Parameter name |Description |
|--			|--									|
|active		|所有组件都支持						|
|active |All components are supported |
|focus		|只有 ```input``` 组件和 ```textarea``` 组件支持|
|focus |Only supported by ```input``` component and ```textarea``` component|
|disabled	|只有 ```input``` 组件和 ```textarea``` 组件支持|
|disabled |Only supported by ```input``` component and ```textarea``` component|
|enabled	|只有 ```input``` 组件和 ```textarea``` 组件支持|
|enabled |Only supported by ```input``` component and ```textarea``` component|
**注意**
**Notice**
> 同时生效的时候，优先级高覆盖优先级低。
> When it takes effect at the same time, the priority is high and the coverage priority is low.
> 例如：```input:active:enabled``` 和 ```input:active``` 同时生效，前者覆盖后者
> For example: ```input:active:enabled``` and ```input:active``` take effect at the same time, the former overrides the latter
- 互联规则如下所示
- The interconnection rules are as follows

<img width="400px" src="https://bjetxgzv.cdn.bspapp.com/VKCEYUGU-dc-site/f3069420-2f17-11eb-8a36-ebb87efcf8c0.png" />


## 线性渐变
## Linear gradient

所有组件均支持线性渐变。[CSS3 渐变](https://www.w3cschool.cn/css3/oj26bfli.html)
All components support linear gradients. [CSS3 Gradient](https://www.w3cschool.cn/css3/oj26bfli.html)
你可以通过  ``` background-image ```属性创建线性渐变。
You can create a linear gradient with the ``` background-image ``` property.
``` javascript
	background-image:linear-gradient(to bottom right,#AD18F9,#05DFC7);
```

只支持两种颜色的渐变，渐变方向如下：
Only two color gradients are supported, and the gradient directions are as follows:
|渐变方向		|描述				|
|Gradient direction |Description |
|--				|--					|
|to right		|从左向右渐变		|
|to right |Fade from left to right |
|to left		|从右向左渐变		|
|to left |Fade from right to left |
|to bottom		|从上到下渐变		|
|to bottom |Gradient from top to bottom |
|to top			|从下到上渐变		|
|to top |Gradient from bottom to top |
|to bottom right|从左上角到右下角	|
|to bottom right|From the upper left corner to the lower right corner |
|to top left	|从右下角到左上角	|
|to top left |From bottom right to top left |
**注意**
**Notice**
> ```background-image``` 优先级高于 ```background-color```，这意味着同时设置 ```background-image``` 和 ```background-color```，```background-color``` 被覆盖。
> ```background-image``` has a higher priority than ```background-color```, which means to set both ``background-image``` and ```background-color```, ` ``background-color``` is overwritten.
> ```background``` 不支持简写。
> ```background``` does not support shorthand.

> **目前暂不支持 radial-gradient（径向渐变）。**
> **Currently, radial-gradient is not supported. **


<img width="300px" src="https://bjetxgzv.cdn.bspapp.com/VKCEYUGU-dc-site/8f70e4e0-308b-11eb-97b7-0dc4655d6e68.PNG" />


## 阴影@boxshadow
## Shadow@boxshadow

### IOS平台：阴影```box-shadow```@ios-box-shadow
### IOS platform: shadow ```box-shadow```@ios-box-shadow
	
	{box-shadow:inset offset-x offset-y blur-radius color}
	{box-shadow:投影方式 X轴偏移量 Y轴偏移量 阴影模糊半径  阴影颜色}
	{box-shadow: projection method X axis offset Y axis offset shadow blur radius shadow color}


|参数			|描述																										|
|Parameter |Description |
|--				|--																											|
|inset（可选）	|默认阴影在边框外。使用 ```inset``` 后，阴影在边框内（即使是透明边框），背景之上内容之下。						|
|inset (optional) |The default shadow is outside the border. After using ```inset```, the shadow is inside the border (even if it is a transparent border), and below the content above the background. |
|offset-x		|设置水平偏移量，如果是负值则阴影位于元素左边。																|
|offset-x |Set the horizontal offset, if it is negative, the shadow will be on the left of the element. |
|offset-y		|设置垂直偏移量，如果是负值则阴影位于元素上面。																|
|offset-y |Set the vertical offset, if it is a negative value, the shadow is on the element. |
|blur-radius	|设置模糊半径，px 单位长度值，值越大，模糊面积越大，阴影就越大越淡。不能为负值。默认为0，此时阴影边缘锐利。	|
|blur-radius | Set the blur radius, px unit length value, the larger the value, the larger the blur area, and the larger and lighter the shadow. Cannot be negative. The default is 0, when the shadow edges are sharp. |
|color			|设置阴影颜色																								|
|color | Set shadow color |

示例
Example
``` css
	.box4 {
	    box-shadow: inset 3px 5px 20px rgb(255, 69, 0);
	}
```

**注意**
**Notice**
- 目前仅 iOS 支持 ```box-shadow``` 属性，Android 暂不支持，可以使用```elevation```或者图片代替。
- Currently only iOS supports the ```box-shadow``` attribute, Android does not currently support it, you can use ```elevation``` or pictures instead.
- 每个元素只支持设置一个阴影效果，不支持多个阴影同时作用于一个元素。
- Each element supports only one shadow effect, and multiple shadows are not supported to act on one element at the same time.


### Android平台：阴影```elevation```@android-box-shadow
### Android platform: shadow ```elevation```@android-box-shadow
Android平台weex对阴影样式(box-shadow)支持不完善，如设置圆角边框时阴影样式显示不正常、设置动画时在Android7上显示不正常、在Android10上出现闪烁现象等。
The Android platform weex has incomplete support for box-shadow. For example, the shadow style is displayed abnormally when the rounded border is set, the display is abnormal on Android7 when the animation is set, and the flicker appears on Android10.
为解决这些问题，从HBuilderX 2.4.7起，新增elevation属性（**组件的属性，不是css样式**）设置组件的层级，Number类型，层级值越大阴影越明显，阴影效果也与组件位置有关，越靠近页面底部阴影效果越明显
In order to solve these problems, starting from HBuilderX 2.4.7, the elevation property (**component property, not css style**) is added to set the level of the component, the Number type, the larger the level value, the more obvious the shadow, and the shadow effect is also related to the component The position is related, the closer to the bottom of the page, the more obvious the shadow effect

	
用法
usage
``` html
	<view elevation="5px"></view>
```


#### 注意
#### Notice
- 设置```elevation```属性产生的阴影暂时无法修改颜色
- The shadow created by setting the ```elevation``` property cannot be modified for the time being
- 设置```elevation```后当前组件的层级会高于其他未设置elevation组件的层级，都设置```elevation```值域越大则层级越高！组件覆盖的场景需要留意
- After setting ```elevation```, the level of the current component will be higher than that of other components without elevation. The higher the value range of ```elevation```, the higher the level! The scene covered by the component needs attention
- 为了避免```elevation```属性的阴影效果与阴影样式(```box-shadow```)冲突，设置```elevation```属性后```box-shadow```样式失效
- In order to avoid conflicts between the shadow effect of the ```elevation``` property and the shadow style (```box-shadow```), set the ```box-shadow`'' style after the ```elevation``` property Invalidation
- 使用```elevation```需要阴影元素的父元素大于阴影范围，否则会对阴影进行裁剪
- Using ```elevation``` requires the parent element of the shadow element to be larger than the shadow range, otherwise the shadow will be clipped
- IOS不支持```elevation```属性，请使用```box-shadow```设置阴影
- IOS does not support the ```elevation``` attribute, please use ```box-shadow``` to set the shadow

## 文本样式
## Text style

### color
color {color}：文字颜色，支持如下字段：
color {color}: text color, supports the following fields:
 * RGB（ rgb(255, 0, 0) ） 
 * RGBA（ rgba(255, 0, 0, 0.5) ） 
 * 十六进制（ #ff0000 ）；
 * Hexadecimal (#ff0000 );
 * 精简写法的十六进制（ #f00 ）
 * Hexadecimal in short form (#f00)
 * 色值关键字（red）
 * Color value keyword (red)

> 只有```text```标签可以设置字体颜色
> Only the ```text``` tag can set the font color

### font-size
font-size {number}：文字大小，只有```text```标签可以设置字体大小
font-size {number}: text size, only ```text``` tag can set the font size

### font-style
font-style {string}：字体类别。可选值 ```normal``` | ```italic```，默认为 ```normal```。
font-style {string}: Font type. Optional value ```normal``` | ```italic```, default is ```normal```.

### font-weight
font-weight {string}：字体粗细程度。默认值: ```normal```；
font-weight {string}: The weight of the font. Default value: ```normal```;

- 可选值: ```normal```, ```bold```, 100, 200, 300, 400, 500, 600, 700, 800, 900
- Optional values: ```normal```, ```bold```, 100, 200, 300, 400, 500, 600, 700, 800, 900
- ```normal``` 等同于 400, ```bold``` 等同于 700；
-```normal``` is equivalent to 400, ```bold``` is equivalent to 700;
- iOS 支持 9 种 ```font-weight```值；Android 仅支持 400 和 700, 其他值会设为 400 或 700
- iOS supports 9 kinds of ```font-weight``` values; Android only supports 400 and 700, other values will be set to 400 or 700
- 类似 ```lighter```, ```bolder``` 这样的值暂时不支持
- Values like ```lighter```, ```bolder``` are temporarily not supported

### text-decoration
```text-decoration {string}```：字体装饰。默认值为 ```none```。
```text-decoration {string}```: Font decoration. The default value is ```none```.

|可选值			|描述						|
|Optional value |Description |
|--				|--							|
|none			|默认。定义标准的文本		|
|none |Default. Defining the standard text |
|underline		|定义文本下的一条线		|
|underline |Define a line under the text |
|line-through	|定义穿过文本下的一条线	|
|line-through |Define a line through the text |

> 只支持 ```text``` 和 ```ricthext```
> Only support ```text``` and ```ricthext```
> 不支持 ```text-decoration:overline```
> Does not support ```text-decoration:overline```

### text-align
```text-align {string}```：对齐方式。默认值为 ```left```。
```text-align {string}```: Alignment. The default value is ```left```.

|可选值	|描述				|
|Optional value |Description |
|--		|--					|
|left	|把文本排列到左边	|
|left | Arrange the text to the left |
|center	|把文本排列到中间	|
|center | Arrange the text to the middle |
|right	|把文本排列到右边|
|right |Arrange the text to the right|
> 不支持```text-align:justify```
> ```text-align:justify`'' is not supported


### font-family

```font-family {string}```：设置字体。这个设置不保证在不同平台，设备间的一致性。
```font-family {string}```: Set the font. This setting does not guarantee consistency between different platforms and devices.

如所选设置在平台上不可用，将会降级到平台默认字体。
If the selected setting is not available on the platform, it will be downgraded to the platform default font.
如果需要加载自定义字体，请参考相关[DOM.addRule](/nvue-api?id=addrule)
If you need to load a custom font, please refer to the related [DOM.addRule](/nvue-api?id=addrule)
### text-overflow

```text-overflow {string}```：设置内容超长时的省略样式。
```text-overflow {string}```: Set the omission style when the content is too long.
|可选值		|描述							|
|Optional value |Description |
|--			|--								|
|clip		|修剪文本						|
|clip | Trim text |
|ellipsis	|显示省略符号来代表被修剪的文本	|
|ellipsis |Display ellipsis to represent trimmed text |
> 只支持 ```text``` 和 ```ricthext```
> Only support ```text``` and ```ricthext```

### lines
```lines {number}```: 正整数，指定最大文本行数，默认```lines```值为0，表示不限制最大行数```lines```。如果文本不够长，实际展示行数会小于指定行数。
```lines {number}```: Positive integer, specify the maximum number of text lines, the default value of ```lines``` is 0, which means that the maximum number of lines ```lines``` is not limited. If the text is not long enough, the actual number of displayed lines will be less than the specified number of lines.
### line-height
line-height {length}: 正整数，每行文字高度。```line-height```是 top 至 bottom的距离。
line-height {length}: A positive integer, the height of each line of text. ```line-height``` is the distance from top to bottom.
```line-height```与```font-size```没有关系，因为```line-height```被 top 和 bottom 所限制，
```line-height``` has nothing to do with ```font-size```, because ```line-height``` is limited by top and bottom,
```font-size``` 被 glyph 所解析。```line-height```和```font-size```相等一般会导致文字被截断。
```font-size``` is parsed by glyph. The equality of ```line-height``` and ```font-size``` will generally cause the text to be truncated.
### word-wrap
```word-wrap:<string>```  对nvue来说 ```anywhere``` 表示在以字符为最小元素做截断换行，其它值或不指定该属性，都以英文单词为单位进行换行。
```word-wrap:<string>``` For nvue, ```anywhere``` means that the character is the smallest element to do truncation and newline, other values or not specifying this attribute, are all in English words as the unit Wrap.

|可选值		|描述								|
|Optional value |Description |
|--			|--									|
|break-word	|在长单词或 URL 地址内部进行换行	|
|break-word |Wrap a line inside a long word or URL address |
|normal		|只在允许的断字点换行				|
|normal |Line breaks only at allowed hyphenation points |
|anywhere	|以字符为最小元素做截断换行	|
|anywhere |Truncate and wrap with characters as the smallest element |
