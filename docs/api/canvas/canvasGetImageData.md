#### uni.canvasGetImageData(OBJECT,this)

返回一个数组，用来描述 canvas 区域隐含的像素数据，在自定义组件下，第二个参数传入自定义组件实例 this，以操作组件内 `<canvas>` 组件。
Return an array to describe the pixel data hidden in the canvas area. Under the custom component, the second parameter is passed into the custom component instance this to operate the `<canvas>` component in the component.

**OBJECT参数说明：**
**OBJECT parameter description:**

|参数|类型|必填|说明|
|Parameter|Type|Required|Description|
|---|---|---|---|
|canvasId|String|是|画布标识，传入 ```<canvas />``` 的 canvas-id（支付宝小程序是id、其他平台是canvas-id）|
|canvasId|String|is|canvas ID, pass in the canvas-id of ```<canvas />``` (Alipay applet is id, other platforms are canvas-id)|
|x|Number|是|将要被提取的图像数据矩形区域的左上角 x 坐标|
|x|Number|is|The x coordinate of the upper left corner of the rectangular area of the image data to be extracted|
|y|Number|是|将要被提取的图像数据矩形区域的左上角 y 坐标|
|y|Number|is|The y coordinate of the upper left corner of the rectangular area of the image data to be extracted|
|width|Number|是|将要被提取的图像数据矩形区域的宽度|
|width|Number|is|The width of the rectangular area of the image data to be extracted|
|height|Number|是|将要被提取的图像数据矩形区域的高度|
|height|Number|is|The height of the rectangular area of the image data to be extracted|
|success|Function|否|接口调用成功的回调函数|
|success|Function|No|Callback function for successful interface call|
|fail|Function|否|接口调用失败的回调函数|
|fail|Function|No|Callback function for interface call failure|
|complete|Function|否|接口调用结束的回调函数（调用成功、失败都会执行）|
|complete|Function|No|Callback function at the end of the interface call (the call will be executed if the call succeeds or fails)|

**success回调返回参数：**
**success callback return parameter:**

|参数|类型|说明|
|Parameter|Type|Description|
|---|---|---|
|errMsg|String||
|errMsg|String||
|width|Number|图像数据矩形的宽度|
|width|Number|The width of the image data rectangle|
|height|Number|图像数据矩形的高度|
|height|Number|The height of the image data rectangle|
|data|Uint8ClampedArray|图像像素点数据，一维数组，每四项表示一个像素点的rgba|
|data|Uint8ClampedArray|Image pixel data, a one-dimensional array, every four items represent the rgba of one pixel|

**示例代码**
**Sample Code**


```javascript
uni.canvasGetImageData({
  canvasId: 'myCanvas',
  x: 0,
  y: 0,
  width: 100,
  height: 100,
  success(res) {
    console.log(res.width) // 100
    console.log(res.height) // 100
    console.log(res.data instanceof Uint8ClampedArray) // true
    console.log(res.data.length) // 100 * 100 * 4
  }
})
```

