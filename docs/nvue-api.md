
## dom


对于那些不依赖 UI 交互的原生功能，nvue将其封装成模块，这是一种通过 javascript 调用原生能力的方法。
For those native functions that do not rely on UI interaction, nvue encapsulates them into modules, which is a way to call native capabilities through javascript.
- uni-app默认内置集成原生模块，如：BindingX，animation， DOM.addRule等。
- uni-app has built-in and integrated native modules by default, such as: BindingX, animation, DOM.addRule, etc.
  通过```uni.requireNativePlugin```引入 App 原生插件
  Introduce native App plugins through ```uni.requireNativePlugin```
  
```js
//使用方式
//How to use
	const PluginName = uni.requireNativePlugin(PluginName); 
	// PluginName 为原生插件名称
	// PluginName is the name of the native plug-in
```
  
  
 - 支持项目nativeplugins目录下和插件市场原生云打包的第三方原生插件。你可以将已有原生模块移植到nvue平台也很方便。
 - Support third-party native plug-ins packaged in the nativeplugins directory of the project and the native cloud of the plug-in market. You can port existing native modules to the nvue platform, which is also very convenient.
  
  使用方式：在manifest.json->App原生插件配置->选择本地插件或者云端插件->打自定义基座才能使用。[详见](/api/extend/native-plugin.md)
  How to use: in manifest.json->App native plug-in configuration->select local plug-in or cloud plug-in->open custom dock to use. [See details](/api/extend/native-plugin.md)
 - nvue还支持uni-app的js API接口，若无特殊说明，则表示vue文件和nvue文件均支持。[详见](/api/README)。
 - nvue also supports the js API interface of uni-app. If there is no special instructions, it means that both vue files and nvue files are supported. [See details](/api/README).
 - nvue 里不支持的 uni-app API，[详见](/nvue-api?id=nvue-里不支持的-uni-app-api)
 - uni-app API not supported in nvue, [see details](/nvue-api?id=nvue-unsupported-uni-app-api)


### addRule

 Weex 提供 DOM.addRule 以**加载自定义字体**。开发者可以通过指定 font-family加载 iconfont 和 custom font。开发者可以使用下面的代码加载自定义字体：
 Weex provides DOM.addRule to **load custom fonts**. Developers can load iconfont and custom font by specifying font-family. Developers can use the following code to load custom fonts:
``` html
	<template>
		<view>
			<text class="my-iconfont">&#xe85c;</text>	
		</view>
	</template>
	<script>
		export default{
			beforeCreate() {
				const domModule = uni.requireNativePlugin('dom')
				domModule.addRule('fontFace', {
					'fontFamily': "myIconfont",
					'src': "url('http://at.alicdn.com/t/font_2234252_v3hj1klw6k9.ttf')"
				});
			}
		}
	</script>
	<style>
		.my-iconfont {
			font-family:myIconfont;
			font-size:60rpx;
			color: #00AAFF;
		}
	</style>
	
	
```

<img width="300px" src="https://bjetxgzv.cdn.bspapp.com/VKCEYUGU-dc-site/18870440-30a9-11eb-bd01-97bc1429a9ff.PNG" />


**addRule(type, contentObject)**
- @fontFace 协议名称，不可修改。
- @fontFace agreement name, cannot be modified.
- @fontFamily ```font-family```的名称。
- @fontFamily ```font-family``` name.
- @src 字体地址，url('') 是保留字段，其参数如下:
	-@src font address, url('') is a reserved field, and its parameters are as follows:
	- http. 从HTTP请求加载, e.g. ```url('http://at.alicdn.com/t/font_1469606063_76593.ttf')```
	- http. Loaded from HTTP request, e.g. ```url('http://at.alicdn.com/t/font_1469606063_76593.ttf')```
	- https. 从HTTPS请求加载, e.g. ```url('https://at.alicdn.com/t/font_1469606063_76593.ttf')```
	- https. Load from HTTPS request, e.g. ```url('https://at.alicdn.com/t/font_1469606063_76593.ttf')```
	- local, Android ONLY. 从assets目录读取, e.g. url('local://foo.ttf'), foo.ttf 是文件名在你的assets目录中.
	- local, Android ONLY. Read from the assets directory, e.g. url('local://foo.ttf'), foo.ttf is the file name in your assets directory.
	- file. 从本地文件读取, e.g. ```url('file://storage/emulated/0/Android/data/com.alibaba.weex/cache/http:__at.alicdn.com_t_font_1469606063_76593.ttf')```
	- file. Read from a local file, eg ```url('file://storage/emulated/0/Android/data/com.alibaba.weex/cache/http:__at.alicdn.com_t_font_1469606063_76593.ttf')` ``
	- data. 从base64读取, e.g. ```url('data:font/truetype;charset=utf-8;base64,AAEAAAALAIAAAwAwR1NVQrD+....')```, 上述data字段不全。
	- data. Read from base64, e.g. ```url('data:font/truetype;charset=utf-8;base64,AAEAAAALAIAAAwAwR1NVQrD+....')```, the above data fields are incomplete.
	
	
	
**注意**
**Notice**
> addRule 方法里的 fontFamily 可以随意取。这个名字不是字体真正的名字。字体真正的名字（font-family），也就是注册到系统中的名字是保存在字体二进制文件中的。你需要确保你使用的字体的真正名字（font-family）足够特殊，否则在向系统注册时可能发生冲突，导致注册失败，你的字符被显示为‘?’。
> The fontFamily in the addRule method can be taken at will. This name is not the real name of the font. The real name of the font (font-family), which is the name registered in the system, is stored in the font binary file. You need to make sure that the real name of the font you use (font-family) is special enough, otherwise there may be conflicts when registering with the system, causing the registration to fail and your characters are displayed as ‘?’.
> 如果你使用 http://www.iconfont.cn/ 来构建你的 iconfont。确保在项目设置中，设置一个特殊的 font-family 名字。默认是 “iconfont”，但极大可能发生冲突。
> If you use http://www.iconfont.cn/ to build your iconfont. Make sure to set a special font-family name in the project settings. The default is "iconfont", but conflicts are likely to occur.
> 调用addRule 在 beforeCreate 中是被推荐的。
> Calling addRule is recommended in beforeCreate.


### scrollToElement<div id="scrollToElement"></div>

让页面滚动到 ref 对应的组件，这个 API 只能用于可滚动组件的子节点，例如 ```<scroller>```，```<list>```, ```<waterfall>``` 等可滚动组件中。
Let the page scroll to the component corresponding to ref. This API can only be used for the child nodes of the scrollable component, such as ```<scroller>```, ```<list>```, ```<waterfall>` `` and other scrollable components.

**scrollToElement(ref, options)**
- @ref，要滚动到的那个节点。
- @ref, the node to scroll to.
- @options
- @options
	- offset，一个到其可见位置的偏移距离，默认是 0。
	- offset, an offset distance to its visible position, the default is 0.
	- animated，是否需要附带滚动动画，默认是 true。
	- animated, whether it needs to be accompanied by a scrolling animation, the default is true.

``` html
  <template>
    <view class="wrapper">
      <scroller class="scroller">
        <view class="row" v-for="(name, index) in rows" :ref="'item'+index">
          <text class="text" :ref="'text'+index">{{name}}</text>
        </view>
      </scroller>
      <view class="group">
        <text @click="goto10" class="button">Go to 10</text>
        <text @click="goto20" class="button">Go to 20</text>
      </view>
    </view>
  </template>
  <script>
    const dom = uni.requireNativePlugin('dom')
    export default {
      data() {
        return {
          rows: []
        }
      },
      created() {
        for (let i = 0; i < 30; i++) {
          this.rows.push('row ' + i)
        }
      },
      methods: {
        goto10(count) {
          const el = this.$refs.item10[0]
          dom.scrollToElement(el, {})
        },
        goto20(count) {
          const el = this.$refs.item20[0]
          dom.scrollToElement(el, {
            offset: 0
          })
        }
      }
    }
  </script>
  <style scoped>
    .scroller {
      width:700rpx;
      height:500px;
      border-width: 3px;
      border-style: solid;
      border-color: rgb(162, 217, 192);
      margin:0 25rpx;
    }
    .row {
      height: 100rpx;
      flex-direction: column;
      justify-content: center;
      padding-left: 30rpx;
      border-bottom-width: 2px;
      border-bottom-style: solid;
      border-bottom-color: #DDDDDD;
    }
    .text {
      font-size: 45rpx;
      color: #666666;
    }
    .group {
      flex-direction: row;
      justify-content: center;
      margin-top: 60rpx;
    }
    .button {
      width: 200rpx;
      padding-top: 20rpx;
      padding-bottom: 20rpx;
      font-size: 40rpx;
      margin-left: 30rpx;
      margin-right: 30rpx;
      text-align: center;
      color: #41B883;
      border-width: 2px;
      border-style: solid;
      border-color: rgb(162, 217, 192);
      background-color: rgba(162, 217, 192, 0.2);
    }
  </style>

```



<img width="300px" src="https://bjetxgzv.cdn.bspapp.com/VKCEYUGU-dc-site/a3478060-33c8-11eb-880a-0db19f4f74bb.gif" />

### getComponentRect

获取某个元素 View 的外框。
Get the outer frame of an element View.
**getComponentRect(ref, callback)**
- @ref，要获取外框的那个节点。
- @ref, to get the node of the outer frame.
- @callback，异步方法，通过回调返回信息。
- @callback, asynchronous method, return information through callback.
回调方法中的数据样例：
Sample data in the callback method:
```html
  {
    result: true,
    size: {
        bottom: 60,
        height: 15,
        left: 0,
        right: 353,
        top: 45,
        width: 353
    }
  }
```



> 此方法需要在节点渲染后调用才能获取正确的信息，可在 mounted 或 更新数据后 updated 中调用
> This method needs to be called after the node is rendered to get the correct information. It can be called in mounted or updated after updating the data

> 如果想要获取到 Weex 视口容器的布局信息，可以指定 ref 为字符串 'viewport'，即 getComponentRect('viewport', callback).
> If you want to get the layout information of the Weex viewport container, you can specify ref as the string'viewport', ie getComponentRect('viewport', callback).


## animation

```animation```模块可以用来在组件上执行动画。JS-Animation可以对组件执行一系列简单的变换 (位置、大小、旋转角度、背景颜色和不透明度)。
The ```animation``` module can be used to perform animations on components. JS-Animation can perform a series of simple transformations (position, size, rotation angle, background color and opacity) of the component.

举个例子，如果有一个```image```组件，通过动画你可以对其进行移动、旋转、拉伸或收缩等动作。
For example, if there is an ```image``` component, you can move, rotate, stretch or shrink it through animation.
```html
  <template>
    <view class="box">
      <view ref="test" @click="move" class="box-item"></view>
    </view>
  </template>
  <script>
      const animation = uni.requireNativePlugin('animation')
      export default {
          methods: {
              move() {
                  var testEl = this.$refs.test;
                  animation.transition(testEl, {
                      styles: {
                          backgroundColor: '#007AFF',
                          transform: 'translate(100px, 80px)',
                          transformOrigin: 'center center'
                      },
                      duration: 800, //ms
                      timingFunction: 'ease',
                      delay: 0 //ms
                  },()=>{
                      uni.showToast({
                          title: 'finished',
                          icon:'none'
                      });
                  })
              }
          }
      }
  </script>
  <style scoped>
    .box{
        width:750rpx;
        height:750rpx;
    }
    .box-item{
      width: 250rpx;
      height: 250rpx;
      background-color: #00aaff;
    }
  </style>
```


<img width="300px" src="https://bjetxgzv.cdn.bspapp.com/VKCEYUGU-dc-site/1852eff0-312d-11eb-8ff1-d5dcf8779628.gif" />




### transition


- @ref，将要执行动画的元素。例如指定动画的元素 ref 属性为 test，可以通过调用 this.$refs.test 来获取元素的引用。
- @ref, the element that will be animated. For example, if the ref attribute of the specified animation element is test, the reference of the element can be obtained by calling this.$refs.test.
- @options，动画参数。
- @options, animation parameters.

下表列出了options所有合法的参数：
The following table lists all the legal parameters of options:

|可选值		|描述		|
|Optional value |Description |
|--			|--			|
|styles	|设置不同样式过渡效果的键值对|
|styles |Set key-value pairs for different style transition effects|
|duration		|指定动画的持续时间 (单位是毫秒)，默认值是 0，表示瞬间达到动画结束状态。																																				|
|duration |Specify the duration of the animation (in milliseconds), the default value is 0, which means that the animation end state is reached instantaneously. |
|delay			|指定请求动画操作到执行动画之间的时间间隔 (单位是毫秒)，默认值是 0，表示没有延迟，在请求后立即执行动画。																												|
|delay |Specify the time interval (in milliseconds) between requesting the animation operation and executing the animation. The default value is 0, which means there is no delay, and the animation will be executed immediately after the request. |
|needLayout		|动画执行是否影响布局，默认值是false。																																													|
|needLayout |Whether the animation execution affects the layout, the default value is false. |
|timingFunction	|描述动画执行的速度曲线，用于描述动画已消耗时间和动画完成进度间的映射关系。默认值是 ```linear```，表示动画从开始到结束都拥有同样的速度。详见下						|
|timingFunction |Describes the speed curve of animation execution, which is used to describe the mapping relationship between the elapsed time of the animation and the progress of the animation. The default value is ```linear```, which means that the animation has the same speed from beginning to end. See below for details |


下表列出了styles所有合法的参数：
The following table lists all the legal parameters of styles:

|可选值		|描述		|
|Optional value |Description |
|--			|--			|
|width	|表示动画执行后应用到组件上的宽度值。如果你需要影响布局，设置needLayout为true。默认值为computed width。|
|width |Indicates the width value applied to the component after the animation is executed. If you need to influence the layout, set needLayout to true. The default value is computed width. |
|height		|表示动画执行后应用到组件上的高度值。如果你需要影响布局，设置设置为 needLayout为true。默认值为computed width。		|
|height | represents the height value applied to the component after the animation is executed. If you need to influence the layout, set the needLayout to true. The default value is computed width. |
|backgroundColor	|动画执行后应用到组件上的背景颜色，默认值为computed backgroundColor。
|backgroundColor |The background color applied to the component after the animation is executed, the default value is computed backgroundColor.
|opacity		|表示动画执行后应用到组件上的不透明度值，默认值为computed opacity。																																						|
|opacity | represents the opacity value applied to the component after the animation is executed, the default value is computed opacity. |
|transformOrigin|`transformOrigin` 定义变化过程的中心点，如transformOrigin: x-axis y-axis 参数 x-axis 可能的值为 left、center、right、长度值或百分比值，参数 y-axis 可能的值为 top、center、bottom、长度值或百分比。默认值为center center。|
|transformOrigin|`transformOrigin` defines the central point of the change process, such as transformOrigin: x-axis y-axis The possible values ​​of x-axis are left, center, right, length or percentage value, and the possible values ​​of y-axis are top, center, bottom, length value or percentage. The default value is center center. |
|transform		| `transform` 变换类型，可能包含rotate，translate，scale及其他属性。默认值为空。详见下																																			|
|transform | `transform` The transformation type, which may include rotate, translate, scale and other attributes. The default value is empty. See below for details |

**transform** 

|可选值							|描述																					|
|Optional value |Description |
|--								|--																						|
|translate/translateX/translateY|指定元素要移动到的位置。单位是长度或百分比，默认值是0.									|
|translate/translateX/translateY|Specify the position where the element is to be moved. The unit is length or percentage, and the default value is 0. |
|rotate/rotateX/rotateY			|v0.16+ 指定元素将被旋转的角度。单位是度 角度度，默认值是0								|
|rotate/rotateX/rotateY |v0.16+ Specifies the angle by which the element will be rotated. The unit is degree angle degree, the default value is 0 |
|scale/scaleX/scaleY			|按比例放大或缩小元素。单位是数字，默认值是1											|
|scale/scaleX/scaleY | Scale up or down the element proportionally. The unit is a number, the default value is 1 |
|perspective					|v0.16+ 观察者距离z=0平面的距离，在Android 4.1及以上有效。单位值数字，默认值为正无穷。	|
|perspective |v0.16+ The distance between the observer and the z=0 plane, valid in Android 4.1 and above. Unit value number, the default value is positive infinity. |


**timingFunction**

|可选值		|描述		|
|Optional value |Description |
|--			|--			|
|linear	|动画从头到尾的速度是相同的	|
|linear |The speed of the animation is the same from beginning to end |
|ease-in		|动画速度由慢到快				|
|ease-in |Animation speed from slow to fast |
|ease-out		|动画速度由快到慢			|
|ease-out |Animation speed from fast to slow |
|ease-in-out		|动画先加速到达中间点后减速到达终点			|
|ease-in-out |The animation first accelerates to the midpoint and then decelerates to the end |
|cubic-bezier(x1, y1, x2, y2)		|在三次贝塞尔函数中定义变化过程，函数的参数值必须处于 0 到 1 之间。更多关于三次贝塞尔的信息请参阅 cubic-bezier 和 Bézier curve。|
|cubic-bezier(x1, y1, x2, y2) |To define the change process in the cubic Bezier function, the parameter value of the function must be between 0 and 1. For more information about cubic-bezier, please refer to cubic-bezier and Bézier curve. |


- @callback，callback是动画执行完毕之后的回调函数。在iOS平台上，你可以获取动画执行是否成功的信息。
- @callback, callback is the callback function after the animation is executed. On the iOS platform, you can get information about whether the animation execution is successful.

**注意**
**Notice**
- iOS上可以获取 ```animation``` 是否执行成功的信息，callback中的result参数会有两种，分别是是Success与Fail。
- On iOS, you can get information about whether ```animation``` is executed successfully. There are two types of result parameters in callback, namely Success and Fail.
- Android 的callback 函数不支持result参数。
- Android's callback function does not support the result parameter.

> 如果需要使用CSS动画，参考[transition](/nvue-css?id=transition)和[transform](/nvue-css?id=transform)。
> If you need to use CSS animation, refer to [transition](/nvue-css?id=transition) and [transform](/nvue-css?id=transform).



## nvue 里使用 BindingX
## Use BindingX in nvue

`uni-app` 是逻辑层和视图层分离的。此时会产生两层通信成本。比如拖动视图层的元素，如果在逻辑层不停接收事件，因为通信损耗会产生不顺滑的体验。
`uni-app` is separated from the logical layer and the view layer. At this time, two layers of communication costs will be incurred. For example, if you drag the elements of the view layer, if you keep receiving events in the logic layer, the communication loss will produce an unsmooth experience.
[BindingX](https://alibaba.github.io/bindingx/) 是weex提供的一种预描述交互语法。由原生解析BindingX规则，按此规则处理视图层的交互和动效。不再实时去js逻辑层运行和通信。
[BindingX](https://alibaba.github.io/bindingx/) is a pre-description interaction syntax provided by weex. The BindingX rule is parsed natively, and the interaction and dynamic effects of the view layer are processed according to this rule. No longer go to the js logic layer to run and communicate in real time.
BindingX类似一种强化版的css，运行性能高，但没有js那样足够强的编程灵活性。
BindingX is similar to an enhanced version of css, with high performance, but not as strong enough in programming flexibility as js.
`uni-app` 内置了 BindingX，可在 `nvue` 中使用 BindingX 完成复杂的动画效果。
`uni-app` has built-in BindingX, which can be used in `nvue` to complete complex animation effects.
- 从HBuilderX 2.3.4起，`uni-app` 编译模式可直接引用 `uni.requireNativePlugin('bindingx')` 模块，weex 模式还需使用 npm 方式引用。
- Starting from HBuilderX 2.3.4, the `uni-app` compilation mode can directly reference the `uni.requireNativePlugin('bindingx')` module, and the weex mode also needs to use npm to reference.
- BindingX demo示例可参考 BindingX 示例里 vue 的相关示例，将实验田里的 vue 代码拷贝到 `nvue` 文件里即可。
- For the BindingX demo example, please refer to the related example of vue in the BindingX example, just copy the vue code in the experimental field to the `nvue` file.

##### 注意
##### Notice
- 暂时不要在 `expression` 内使用 `origin` 
- Don't use `origin` in `expression` for now

##### 代码示例:
##### Code example:

```html
	<template>
	    <div class="container">
	        <div ref="b1" class="btn" style="background-color:#6A1B9A" @click="clickBtn">
	            <text class="text">A</text>
	        </div>
	        <div ref="b2" class="btn" style="background-color:#0277BD" @click="clickBtn">
	            <text class="text">B</text>
	        </div>
	        <div ref="b3" class="btn" style="background-color:#FF9800" @click="clickBtn">
	            <text class="text">C</text>
	        </div>
	        <div ref="main_btn" class="btn" @click="clickBtn">
	            <image class="image" ref="main_image" src="https://gw.alicdn.com/tfs/TB1PZ25antYBeNjy1XdXXXXyVXa-128-128.png" />
	        </div>
	    </div>
	</template>
	<script>
	    const Binding = uni.requireNativePlugin('bindingx');
	    module.exports = {
	        data() {
	            return {
	                isExpanded: false
	            }
	        },
	        methods: {
	            getEl: function(el) {
	                if (typeof el === 'string' || typeof el === 'number') return el;
	                if (WXEnvironment) {
	                    return el.ref;
	                } else {
	                    return el instanceof HTMLElement ? el : el.$el;
	                }
	            },
	            collapse: function() {
	                let main_btn = this.getEl(this.$refs.main_btn);
	                let main_image = this.getEl(this.$refs.main_image);
	                let b1 = this.getEl(this.$refs.b1);
	                let b2 = this.getEl(this.$refs.b2);
	                let b3 = this.getEl(this.$refs.b3);
	                let main_binding = Binding.bind({
	                    eventType: 'timing',
	                    exitExpression: 't>800',
	                    props: [{
	                        element: main_image,
	                        property: 'transform.rotateZ',
	                        expression: 'easeOutQuint(t,45,0-45,800)'
	
	                    }, {
	                        element: main_btn,
	                        property: 'background-color',
	                        expression: "evaluateColor('#607D8B','#ff0000',min(t,800)/800)"
	                    }]
	                }, function(res) {
	                    if (res.state === 'exit') {
	                        Binding.unbind({
	                            token: main_binding.token,
	                          eventType: 'timing'
	                        })
	                    }
	                });
	                let btn_binding = Binding.bind({
	                    eventType: 'timing',
	                    exitExpression: 't>800',
	                    props: [{
	                        element: b1,
	                        property: 'transform.translateY',
	                        expression: "easeOutQuint(t,-150,150,800)"
	                    }, {
	                        element: b2,
	                        property: 'transform.translateY',
	                        expression: "t<=100?0:easeOutQuint(t-100,-300,300,700)"
	                    }, {
	                        element: b3,
	                        property: 'transform.translateY',
	                        expression: "t<=200?0:easeOutQuint(t-200,-450,450,600)"
	                    }]
	                }, function(res) {
	                    if (res.state === 'exit') {
	                        Binding.unbind({
	                            token: btn_binding.token,
	                          eventType: 'timing'
	                        })
	                    }
	                })
	            },
	            expand: function() {
	                let main_btn = this.getEl(this.$refs.main_btn);
	                let main_image = this.getEl(this.$refs.main_image);
	                let b1 = this.getEl(this.$refs.b1);
	                let b2 = this.getEl(this.$refs.b2);
	                let b3 = this.getEl(this.$refs.b3);
	                let main_binding = Binding.bind({
	                    eventType: 'timing',
	                    exitExpression: 't>100',
	                    props: [{
	                        element: main_image,
	                        property: 'transform.rotateZ',
	                        expression: 'linear(t,0,45,100)'
	                    }, {
	                        element: main_btn,
	                        property: 'background-color',
	                        expression: "evaluateColor('#ff0000','#607D8B',min(t,100)/100)"
	                    }]
	                }, function(res) {
	                    if (res.state === 'exit') {
	                        Binding.unbind({
	                            token: main_binding.token,
	                          eventType: 'timing'
	                        })
	                    }
	                });
	                let btn_binding = Binding.bind({
	                    eventType: 'timing',
	                    exitExpression: 't>800',
	                    props: [{
	                        element: b1,
	                        property: 'transform.translateY',
	                        expression: "easeOutBounce(t,0,0-150,800)"
	                    }, {
	                        element: b2,
	                        property: 'transform.translateY',
	                        expression: "t<=100?0:easeOutBounce(t-100,0,0-300,700)"
	                    }, {
	                        element: b3,
	                        property: 'transform.translateY',
	                        expression: "t<=200?0:easeOutBounce(t-200,0,0-450,600)"
	                    }]
	                }, function(res) {
	                    if (res.state === 'exit') {
	                        Binding.unbind({
	                            token: btn_binding.token,
	                          eventType: 'timing'
	                        })
	                    }
	                })
	            },
	            clickBtn: function(e) {
	                if (this.isExpanded) {
	                    this.collapse();
	                } else {
	                    this.expand();
	                }
	                this.isExpanded = !this.isExpanded;
	            }
	        }
	    }
	</script>
	<style>
	    .container {
	        flex: 1;
	    }
	    .image {
	        width: 60px;
	        height: 60px;
	    }
	    .text {
	        color: #ffffff;
	        font-size: 30px;
	    }
	    .btn {
	        width: 100px;
	        height: 100px;
	        background-color: #ff0000;
	        align-items: center;
	        justify-content: center;
	        position: absolute;
	        border-radius: 50px;
	        bottom: 25px;
	        right: 25px;
	    }
	</style>
```

<img width="300px" src="https://bjetxgzv.cdn.bspapp.com/VKCEYUGU-dc-site/6c9f84b0-30a6-11eb-880a-0db19f4f74bb.gif" />






## nvue 和 vue 相互通讯@communication
## nvue and vue communicate with each other @communication

在 uni-app 中，nvue 和 vue 页面可以混搭使用。
In uni-app, nvue and vue pages can be mixed and used.

推荐使用 ```uni.$on``` , ```uni.$emit``` 的方式进行页面通讯，旧的通讯方式（uni.postMessage及plus.webview.postMessageToUniNView）不再推荐使用。
It is recommended to use ```uni.$on```, ```uni.$emit``` for page communication. The old communication methods (uni.postMessage and plus.webview.postMessageToUniNView) are no longer recommended.

##### 通讯实现方式
##### Communication realization method

```javascript
	// 接收信息的页面
	// page to receive information
	// $on(eventName, callback)  
	uni.$on('page-popup', (data) => {  
	    console.log('标题：' + data.title)
	    console.log('内容：' + data.content)
	})  
	
	// 发送信息的页面
	// page to send information
	// $emit(eventName, data)  
	uni.$emit('page-popup', {  
	    title: '我是title',  
	    content: '我是content'  
	});
```

**使用此页面通讯时注意事项：要在页面卸载前，使用 uni.$off 移除事件监听器。**[参考](https://uniapp.dcloud.io/collocation/frame/communication?id=off)
**Notes when using this page for communication: Use uni.$off to remove the event listener before the page is uninstalled. **[Reference](https://uniapp.dcloud.io/collocation/frame/communication?id=off)

### nvue 向 vue 通讯（已过期，推荐使用上面的uni.$on、uni.$emit）
### nvue to vue communication (expired, recommended to use uni.$on, uni.$emit above)

##### 步骤：
##### Steps:

1. 在 nvue 使用 uni.postMessage(data) 发送数据通讯，data 为 JSON 格式（键值对的值仅支持String）。
1. Use uni.postMessage(data) to send data communication in nvue, data is in JSON format (key-value pair values only support String).

2. 在 App.vue 里使用 onUniNViewMessage 进行监听。
2. Use onUniNViewMessage to monitor in App.vue.

##### 代码示例:
##### Code example:

```html
	//test.nvue
	<template>
	    <view @click="test">
	        <text>点击页面发送数据</text>
			<text>Click the page to send data</text>
	    </view>
	</template>
	<script>
	    export default {
	        methods: {
	            test(e) {
	                uni.postMessage({test: "数据(data)",value:"数据(data)"});
	            }
	        }
	    }
	</script>
```

```html
	//App.vue
	<script>
	    export default {
	        onUniNViewMessage:function(e){
				console.log("App.vue收到数据")
				console.log("App.vue received data")
				console.log(JSON.stringify(e.data))  
	        },
	        onLaunch: function() {
	            console.log('App Launch');
	        }
	    }
	</script>
```


### vue 向 nvue 通讯（已过期，推荐使用上面的uni.$on、uni.$emit）
### Communication from vue to nvue (expired, recommended to use uni.$on, uni.$emit above)

##### 步骤：
##### Steps:

1. 在 ```vue``` 里使用 ```plus.webview.postMessageToUniNView(data,nvueId)``` 发送消息，```data``` 为 ```JSON``` 格式（键值对的值仅支持String），```nvueId``` 为 ```nvue``` 所在 webview 的 id，webview的 id 获取方式参考：[$getAppWebview()](https://uniapp.dcloud.net.cn/collocation/frame/window?id=getappwebview)。
1. Use ```plus.webview.postMessageToUniNView(data,nvueId)``` in ```vue``` to send a message, ```data``` is ```JSON``` format (key value The value of the pair only supports String), ```nvueId``` is the id of the webview where ```nvue``` is located. For the method of obtaining the id of the webview, please refer to: [$getAppWebview()](https://uniapp.dcloud. net.cn/collocation/frame/window?id=getappwebview).

2. 在 ```nvue``` 里引用 ```globalEvent``` 模块监听 ```plusMessage``` 事件，如下： 
2. Use the ```globalEvent``` module to monitor the ```plusMessage``` event in ```nvue```, as follows:

```javascript
	const globalEvent = uni.requireNativePlugin('globalEvent');
	globalEvent.addEventListener("plusMessage", e => {
		console.log(e.data);
		//得到数据
		//Get data
	});
```

##### 代码示例:

```javascript
	//index.nvue
	<template>
	    <div @click="test">
	        <text>点击页面发送数据{{num}}</text>
			<text>Click the page to send data{{num}}</text>
	    </div>
	</template>
	<script>
	    const globalEvent = uni.requireNativePlugin('globalEvent');
	    export default {
	        data() {
	            return {
	                num: "0"
	            }
	        },
	        created() {
	            globalEvent.addEventListener("plusMessage", e => {
	                console.log(e.data);
	                if (e.data.num) { 
						//存在num时才赋值，在nvue里调用uni的API也会触发plusMessage事件，所以需要判断需要的数据是否存在
	                    // Assign a value when num exists. Calling uni API in nvue will also trigger the plusMessage event, so it is necessary to determine whether the required data exists
						this.num = e.data.num
	                }
	            });
	        },
	        methods: {
	            test(e) {
	                uni.navigateTo({
	                    url: '../test/test'
	                })
	            }
	        }
	    }
```

```html
	//test.vue
	<template>
	    <view>
	        <button type="primary" @click="test">点击改变nvue的数据</button>
			<button type="primary" @click="test">click to change the data of nvue</button>
	    </view>
	</template>
	<script>
	    export default {
	        methods: {
	            test() {
	                var pages = getCurrentPages();
	                var page = pages[pages.length - 2];
	                var currentWebview = page.$getAppWebview();
	                plus.webview.postMessageToUniNView({
	                    num: "123"
	                }, currentWebview.id);
	                uni.navigateBack()
	            }
	        }
	    }
	</script>
```




## vue 和 nvue 共享的变量和数据@sharevar
## Variables and data shared by vue and nvue@sharevar

除了通信事件，vue 和 nvue 页面之间还可以共享变量和存储。 ```uni-app```提供的共享变量和数据的方案如下：
In addition to communication events, variables and storage can also be shared between vue and nvue pages. The scheme of shared variables and data provided by ```uni-app``` is as follows:

1. **vuex:** 自HBuilderX 2.2.5起，nvue支持```vuex```。这是vue官方的状态管理工具。
1. **vuex:** Since HBuilderX 2.2.5, nvue supports ```vuex```. This is the official state management tool of vue.

> 注意：不支持直接引入```store```使用，可以使用```mapState```、```mapGetters```、```mapMutations```等辅助方法或者使用```this.$store```
> Note: Directly importing ```store``` is not supported, you can use ```mapState```, ```mapGetters```, ```mapMutations``` and other auxiliary methods or use ```this .$store```

2. **uni.storage:**
	
	
	- vue和nvue页面可以使用相同的```uni.storage```存储。这个存储是持久化的。 比如登录状态可以保存在这里。
	- Both vue and nvue pages can use the same ```uni.storage``` storage. This storage is persistent. For example, the login status can be saved here.
	
	- App端还支持```plus.sqlite```，也是共享通用的。
	- App also supports ```plus.sqlite```, which is also common for sharing.

3. **globalData:** ```globalData```机制全端通用。 在App.vue文件里定义```globalData```，如下：
3. **globalData:** ```globalData``` mechanism is universal. Define ```globalData``` in the App.vue file as follows:

```javascript
	<script>  
	    export default {  
	        globalData: {  
	            text: 'text'  
	        },  
	        onLaunch: function() {  
	            console.log('App Launch')  
	        },  
	        onShow: function() {  
	            console.log('App Show')  
	        },  
	        onHide: function() {  
	            console.log('App Hide')  
	        }  
	    }  
	</script>
```


- js中操作```globalData```的方式如下： ```getApp().globalData.text = 'test'```
- The way to operate ```globalData``` in js is as follows: ```getApp().globalData.text ='test'```

- 如果需要把```globalData```的数据绑定到页面上，可在页面的onShow声明周期里进行变量重赋值。
- If you need to bind the data of ```globalData``` to the page, you can perform variable reassignment during the onShow statement cycle of the page.





## nvue 里使用 HTML5Plus API
## Use HTML5Plus API in nvue

nvue页面可直接使用plus的API，并且不需要等待plus ready。
The nvue page can directly use the plus API, and there is no need to wait for plus ready.

## nvue 里不支持的 uni-app API
## uni-app API not supported in nvue

nvue 支持大部分 uni-app API ，下面只列举目前还**不支持的 API** 。
nvue supports most uni-app APIs. Below are only the APIs that are currently **unsupported**.


##### 动画
##### Animation

|API		|说明		|解决方案|
|API |Description |Solution|
|--			|--			|--			|
|uni.createAnimation()	|创建一个动画实例	|[animation](/nvue-api?id=animation)|
|uni.createAnimation() |Create an animation instance |[animation](/nvue-api?id=animation)|

##### 滚动
##### Scroll
|API		|说明		|解决方案|
|--			|--			|--			|
|uni.pageScrollTo()	|将页面滚动到目标位置	|[scrollToElement](#scrollToElement)|
|uni.pageScrollTo() |Scroll the page to the target position |[scrollToElement](#scrollToElement)|

##### 节点布局交互
##### Node layout interaction
|API		|说明		|
|API |Description |Solution|
|--			|--			|
|uni.createIntersectionObserver()	|创建并返回一个 IntersectionObserver 对象实例	|
|uni.createIntersectionObserver() |Create and return an IntersectionObserver object instance |
##### 绘画
##### Painting
canvas API使用，[详见canvas文档](https://uniapp.dcloud.net.cn/api/canvas/createCanvasContext)。
Canvas API use, [see canvas document for details](https://uniapp.dcloud.net.cn/api/canvas/createCanvasContext).
