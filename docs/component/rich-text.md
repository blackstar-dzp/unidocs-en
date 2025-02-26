#### rich-text
富文本。
Rich text.

**属性说明**
**Property description**

|属性名|类型|默认值|说明|平台兼容|
| Attribute name | Types of| Defaults | Description|Platform Compatibility|
|:-|:-|:-|:-|:-|
|nodes|Array / String|[]|节点列表 / HTML String||
| nodes          | Array / String | []       | Node list / HTML String ||


**注意**
**note**

- app-nvue 平台 nodes 属性只支持使用 Array 类型
- The app-nvue platform nodes property only supports the Array type


如果需要支持 HTML String，则需要自己将 HTML String转化为 nodes 数组，可使用 [html-parser](https://github.com/dcloudio/hello-uniapp/blob/master/common/html-parser.js) 转换。
If you need to support HTML String, you need to convert HTML String to nodes array by yourself, you can use [html-parser](https://github.com/dcloudio/hello-uniapp/blob/master/common/html-parser.js) to convert.

支持默认事件，包括：click、touchstart、touchmove、touchcancel、touchend、longpress。
Support default events, including: click, touchstart, touchmove, touchcancel, touchend, longpress.

**nodes 属性推荐使用 Array 类型，由于组件会将 String 类型转换为 Array 类型，因而性能会有所下降。**
**The Array type is recommended for the nodes attribute. Since the component converts the String type to the Array type, the performance will decrease.**

##### nodes

现支持两种节点，通过 type 来区分，分别是元素节点和文本节点，默认是元素节点，在富文本区域里显示的 HTML 节点。
Now supports two kinds of nodes, distinguished by type, which are element node and text node. The default is element node, which is the HTML node displayed in the rich text area.

**元素节点：type = node**
**Element node: type = node**

|属性|说明|类型|必填|备注|
| Attributes | Description| Types of | Required | Remarks|
|:-|:-|:-|:-|:-|
|name|标签名|String|是|支持部分受信任的 HTML 节点|
| name       | Label name      | String   | Yes      | Support for partially trusted HTML nodes                    |
|attrs|属性|Object|否|支持部分受信任的属性，遵循 Pascal 命名法|
| attrs      | Attributes      | Object   | no       | Support some trusted attributes, follow Pascal nomenclature |
|children|子节点列表|Array|否|结构和 nodes 一致|
| children   | Child node list | Array    | no       | The structure is consistent with nodes                      |

**文本节点：type = text**
**Text node: type = text**

|属性|说明|类型|必填|备注|
| Attributes | Description | Types of | Required | Remarks          |
|:-|:-|:-|:-|:-|
|text|文本|String|是|支持 entities|
| text       | text        | String   | Yes      | Support entities |
 
##### 受信任的HTML节点及属性
##### Trusted HTML nodes and attributes

全局支持class和style属性，**不支持id属性**。
The class and style attributes are globally supported, **but the id attribute is not supported** .

|节点|属性|
| node       | Attributes                      |
|:-|:-|
|a||
|abbr||
|b||
|blockquote||
|br||
|code||
|col|span，width|
|colgroup|span，width|
|dd||
|del||
|div||
|dl||
|dt||
|em||
|fieldset||
|h1||
|h2||
|h3||
|h4||
|h5||
|h6||
|hr||
|i||
|img|alt，src，height，width|
|ins||
|label||
|legend||
|li||
|ol|start，type|
|p||
|q||
|span||
|strong||
|sub||
|sup||
|table|width|
|tbody||
|td|colspan，height，rowspan，width|
|tfoot||
|th|colspan，height，rowspan，width|
|thead||
|tr||
|ul|&nbsp;|

**示例** [查看演示](https://hellouniapp.dcloud.net.cn/pages/component/rich-text/rich-text)
**Example** [View Demo](https://hellouniapp.dcloud.net.cn/pages/component/rich-text/rich-text)

以下示例代码，来自于[hello uni-app项目](https://github.com/dcloudio/hello-uniapp)，推荐使用HBuilderX，新建uni-app项目，选择hello uni-app模板，可直接体验完整示例。
The following sample code comes from the hello uni-app project . It is recommended to use HBuilderX to create a new uni-app project and choose the hello uni-app template to directly experience the complete example.
```html
<!-- This example does not include the complete css, please refer to the above to obtain the external css, check it in the hello uni-app project -->
<template>
	<view class="content">
		<page-head :title="title"></page-head>
		<view class="uni-padding-wrap">
			<view class="uni-title uni-common-mt">
				Array
				<text>\nThe nodes attribute is Array</text>
			</view>
			<view class="uni-common-mt" style="background:#FFF; padding:20rpx;">
				<rich-text :nodes="nodes"></rich-text>
			</view>
			<view class="uni-title uni-common-mt">
				String
				<text>\nThe nodes attribute is String</text>
			</view>
			<view class="uni-common-mt" style="background:#FFF; padding:20rpx;">
				<rich-text :nodes="strings"></rich-text>
			</view>
		</view>
	</view>
</template>
```
```javascript
export default {
    data() {
        return {
            nodes: [{
                name: 'div',
                attrs: {
                    class: 'div-class',
                    style: 'line-height: 60px; color: red; text-align:center;'
                },
                children: [{
                    type: 'text',
                    text: 'Hello&nbsp;uni-app!'
                }]
            }],
            strings: '<div style="text-align:center;"><img src="https://bjetxgzv.cdn.bspapp.com/VKCEYUGU-uni-app-doc/d8590190-4f28-11eb-b680-7980c8a877b8.png"/></div>'
        }
    }
}
```

![uniapp](https://bjetxgzv.cdn.bspapp.com/VKCEYUGU-uni-app-doc/ef5ba530-4f2f-11eb-bdc1-8bd33eb6adaa.png)

**Tips**

- nodes 不推荐使用 String 类型，性能会有所下降。
- The String type is not recommended for nodes, and performance will decrease.
- rich-text 组件内屏蔽所有节点的事件。所以如果内容中有链接、图片需要点击，则不能使用rich-text，此时可在[uni-app插件市场](https://ext.dcloud.net.cn/search?q=parse)搜索parse插件使用。app-nvue的rich-text组件支持链接图片点击。
- The rich-text component shields the events of all nodes. Therefore, if there are links or images in the content that need to be clicked, rich-text cannot be used. At this time, you can search for the parse plugin in the [uni-app plugin market](https://ext.dcloud.net.cn/search?q=parse) . The rich-text component of app-nvue supports click on link images.
- attrs 属性不支持 id ，支持 class 。
- The attrs attribute does not support id, but supports class.
- name 属性大小写不敏感。
- The name attribute is not case sensitive.
- 如果使用了不受信任的HTML节点，该节点及其所有子节点将会被移除。
- If an untrusted HTML node is used, the node and all its children will be removed.
- img 标签仅支持网络图片。
- The img tag only supports web pictures.
- 如果在自定义组件中使用 rich-text 组件，那么仅自定义组件的 css 样式对 rich-text 中的 class 生效。
- If the rich-text component is used in the custom component, only the css style of the custom component will take effect for the class in the rich-text.
