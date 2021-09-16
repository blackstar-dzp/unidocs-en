### uni.setScreenBrightness(OBJECT)
设置屏幕亮度。
Screen brightness setting.

**平台差异说明**
**Platform difference description**

|App|H5|
|:-:|:-:|
|√|x|

**OBJECT 参数说明**
**OBJECT Parameter description**

|参数名|类型|必填|说明|
|Attribute|Type|Required|Description|
|:-|:-|:-|:-|
|value|Number|是|屏幕亮度值，范围 0~1，0 最暗，1 最亮|
|value|Number|yes|Screen brightness value,Ranges 0 to 1, where 0 is darkest and 1 is brightest|
|success|Function|否|接口调用成功的回调|
|success|Function|no|Callback function for successful interface call|
|fail|Function|否|接口调用失败的回调函数|
|fail|Function|no|Callback function for interface call failure|
|complete|Function|否|接口调用结束的回调函数（调用成功、失败都会执行）|
|complete|Function|no|The callback function for the end of the interface call (the call will be executed if it succeeds or fails)|

**示例**
**Example**

```javascript
uni.setScreenBrightness({
	value: 0.5,
	success: function () {
		console.log('success');
	}
});
```

>*Tips:* 避免 onshow() 里使用 setScreenBrightness() , 亮度变化会再次触发 onShow() 造成死循环
>*Tips:* avoid using setScreenBrightness() in onshow() process, The brightness change triggers onShow() again, causing an endless loop

### uni.getScreenBrightness(OBJECT)
获取屏幕亮度。
Get screen brightness value.

**平台差异说明**
**Platform difference description**


|App|H5|
|:-:|:-:|
|√|x|

**OBJECT 参数说明**
**OBJECT Parameter description**

|参数名|类型|必填|说明|
|Attribute|Type|Required|Description|
|:-|:-|:-|:-|
|success|Function|否|接口调用成功的回调|
|success|Function|no|Callback function for successful interface call|
|fail|Function|否|接口调用失败的回调函数|
|fail|Function|no|Callback function for interface call failure|
|complete|Function|否|接口调用结束的回调函数（调用成功、失败都会执行）|
|complete|Function|no|The callback function for the end of the interface call (the call will be executed if it succeeds or fails)|

**success 返回参数说明**
**success Return parameter description**

|参数|类型|说明|
|Parameter|Type|Description|
|:-|:-|:-|
|value|Number|屏幕亮度值，范围 0~1，0 最暗，1 最亮。|
|value|Number|Screen brightness values, ranging from 0 to 1, where 0 is darkest and 1 is brightest.|

**示例**
**Example**

```javascript
uni.getScreenBrightness({
	success: function (res) {
		console.log('屏幕亮度值：' + res.value);
		console.log('Screen brightness value:' + res.value);
	}
});
```

### uni.setKeepScreenOn(OBJECT)
设置是否保持常亮状态。仅在当前应用生效，离开应用后设置失效。
Sets whether to remain always on. This will only take effect in the current application, and will not work when you leave the application.

**平台差异说明**
**Platform difference description**

|App|H5|
|:-:|:-:|
|√|x|

**OBJECT 参数说明**
**OBJECT Parameter description**

|参数名|类型|必填|说明|
|Attribute|Type|Required|Description|
|:-|:-|:-|:-|
|keepScreenOn|Boolean|是|是否保持屏幕常亮|
|keepScreenOn|Boolean|yes|Whether to keep the screen always on|
|success|Function|否|接口调用成功的回调|
|success|Function|no|Callback function for successful interface call|
|fail|Function|否|接口调用失败的回调函数|
|fail|Function|no|Callback function for interface call failure|
|complete|Function|否|接口调用结束的回调函数（调用成功、失败都会执行）|
|complete|Function|no|The callback function for the end of the interface call (the call will be executed if it succeeds or fails)|

**success 返回参数说明**
**success Return parameter description**

|参数|类型|说明|
|Parameter|Type|Description|
|:-|:-|:-|
|errMsg|String|调用结果|
|errMsg|String|The results|

**示例**

```javascript
// 保持屏幕常亮
// Keep the screen always on
uni.setKeepScreenOn({
	keepScreenOn: true
});
```

