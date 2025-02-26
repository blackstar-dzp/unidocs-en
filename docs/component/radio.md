#### radio-group

单项选择器，内部由多个 ``<radio>`` 组成。通过把多个`radio`包裹在一个`radio-group`下，实现这些`radio`的单选。
Single selector, a plurality of internal `<radio>`components. By putting multiple `radio`packages under one `radio-group`, `radio`the single selection of these is realized .

**属性说明**
**Property description**

|属性名|类型|默认值|说明|
| Attribute name | Types of    | Defaults | Description                                                  |
|:-|:-|:-|:-|
|@change|EventHandle||``<radio-group>`` 中的选中项发生变化时触发 change 事件，event.detail = {value: 选中项radio的value}|
| @change        | EventHandle |          | `<radio-group>` The change event is triggered when the selected item in the selection changes, event.detail = {value: the value of the selected item radio} |

#### radio

单选项目。
Single-select items.

**属性说明**
**Property description**

|属性名|类型|默认值|说明|
| Attribute name | Types of | Defaults | Description                                                  |
|:-|:-|:-|:-|
|value|String||``<radio>`` 标识。当该 ``<radio>`` 选中时，``<radio-group>`` 的 change 事件会携带 ``<radio>`` 的 value|
| value          | String   |          | `<radio>`Logo. When the `<radio>`time is selected, `<radio-group>`a change event will carry `<radio>`a value |
|checked|Boolean|false|当前是否选中|
| checked        | Boolean  | false    | Is currently selected                                        |
|disabled|Boolean|false|是否禁用|
| disabled       | Boolean  | false    | Whether to disable                                           |
|color|Color||radio的颜色，同css的color|
| color          | Color    |          | The color of radio, same as the color of css                 |

**示例** [查看演示](https://hellouniapp.dcloud.net.cn/pages/component/radio/radio)
 **Example** [View Demo](https://hellouniapp.dcloud.net.cn/pages/component/radio/radio)
 
以下示例代码，来自于[hello uni-app项目](https://github.com/dcloudio/hello-uniapp)，推荐使用HBuilderX，新建uni-app项目，选择hello uni-app模板，可直接体验完整示例。
The following sample code comes from [hello uni-app project](https://github.com/dcloudio/hello-uniapp), it is recommended to use HBuilderX, create a new uni-app project, choose hello uni-app template, you can experience the complete Example.
```html
<!-- 本示例未包含完整css，获取外链css请参考上文，在hello uni-app项目中查看 -->
<template>
	<view>
		<view class="uni-padding-wrap">
			<view class="uni-title">Default style</view>
			<view>
				<label class="radio"><radio value="r1" checked="true" />Selected</label>
				<label class="radio"><radio value="r2" />Unselected</label>
			</view>
		</view>
		<view class="uni-title uni-common-mt uni-common-pl">Recommended display style</view>
		<view class="uni-list">
			<radio-group @change="radioChange">
				<label class="uni-list-cell uni-list-cell-pd" v-for="(item, index) in items" :key="item.value">
					<view>
						<radio :value="item.value" :checked="index === current" />
					</view>
					<view>{{item.name}}</view>
				</label>
			</radio-group>
		</view>
	</view>
</template>
```
```javascript
export default {
    data() {
        return {
            items: [{
                    value: 'USA',
                    name: 'USA'
                },
                {
                    value: 'CHN',
                    name: 'China',
                    checked: 'true'
                },
                {
                    value: 'BRA',
                    name: 'Brazil'
                },
                {
                    value: 'JPN',
                    name: 'Japan'
                },
                {
                    value: 'ENG',
                    name: 'England'
                },
                {
                    value: 'FRA',
                    name: 'France'
                },
            ],
            current: 0
        }
    },
    methods: {
        radioChange: function(evt) {
            for (let i = 0; i < this.items.length; i++) {
                if (this.items[i].value === evt.detail.value) {
                    this.current = i;
                    break;
                }
            }
        }
    }
}
```
 
![uniapp](https://bjetxgzv.cdn.bspapp.com/VKCEYUGU-uni-app-doc/44bec6b0-4f30-11eb-a16f-5b3e54966275.png)


**注意**
**Notice**
- 如需调节radio大小，可通过css的scale方法调节，如缩小到70%`style="transform:scale(0.7)"`
- -If you need to adjust the radio size, you can adjust it through the scale method of CSS, such as reducing it to 70% `style="transform:scale(0.7)"`
- radio不是checkbox，点击一个已经选中的radio，不会将其取消选中
-The radio is not a checkbox. Clicking on a radio that has been selected will not deselect it

**扩展**
**Extensions**
- uni-ui提供了增强的uni-data-checkbox组件，基于[datacom规范](/component/datacom)，只需传入data数据，即可自动生成一组单选框，使用方式更简洁，并且支持[uni-forms](https://ext.dcloud.net.cn/plugin?id=2773)的表单验证。uni-data-checkbox组件详见[https://ext.dcloud.net.cn/plugin?id=3456](https://ext.dcloud.net.cn/plugin?id=3456)
-uni-ui provides an enhanced uni-data-checkbox component. Based on the [datacom specification](/component/datacom), you only need to pass in data data to automatically generate a set of radio buttons. The usage is more concise, and Support [uni-forms](https://ext.dcloud.net.cn/plugin?id=2773) form verification. For details of uni-data-checkbox components, please refer to [https://ext.dcloud.net.cn/plugin?id=3456](https://ext.dcloud.net.cn/plugin?id=3456)
