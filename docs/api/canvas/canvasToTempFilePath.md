#### uni.canvasToTempFilePath(object, component)

把当前画布指定区域的内容导出生成指定大小的图片，并返回文件路径。在自定义组件下，第二个参数传入自定义组件实例，以操作组件内 `<canvas>` 组件。
Export the contents of the specified area of the current canvas to generate a picture of the specified size, and return the file path. Under the custom component, the second parameter is passed into the custom component instance to operate the `<canvas>` component in the component.

**平台差异说明**
**Platform difference description**

|App|H5|
|:-:|:-:|
|√|√|

**object参数说明：**
**Object parameter description:**

|参数	|类型		|必填		|说明	|
|Parameter |Type |Required |Description |
|---|---|---|---|
|x	|Number		|否			|画布x轴起点（默认0）|					
|x |Number |No |Start of canvas x-axis (default 0)|
|y	|Number		|否			|画布y轴起点（默认0）|					
|y |Number |No |Start point of canvas y-axis (default 0)|
|width	|Number		|否			|画布宽度（默认为canvas宽度-x）|					
|width |Number |No |Canvas width (default is canvas width-x)|
|height	|Number		|否			|画布高度（默认为canvas高度-y）|					
|height |Number |No |Canvas height (default is canvas height-y)|
|destWidth	|Number		|否			|输出图片宽度（默认为 width * 屏幕像素密度）|					
|destWidth |Number |No |Output image width (default is width * screen pixel density)|
|destHeight	|Number		|否			|输出图片高度（默认为 height * 屏幕像素密度）|					
|destHeight |Number |No |The height of the output image (the default is height * screen pixel density)|
|canvasId	|String		|是			|画布标识，传入 ``<canvas/>`` 的 canvas-id（支付宝小程序是id、其他平台是canvas-id）|						
|canvasId |String |Yes |Canvas ID, pass in the canvas-id of ``<canvas/>`` (Alipay applet is id, other platforms are canvas-id)|
|fileType	|String		|否			|目标文件的类型，只支持 'jpg' 或 'png'。默认为 'png'|		
|fileType |String |No |The type of the target file, only'jpg' or'png' is supported. The default is'png'|
|quality	|Number		|否			|图片的质量，取值范围为 (0, 1]，不在范围内时当作1.0处理|		
|quality |Number |No |The quality of the picture. The value range is (0, 1]. If it is not in the range, it will be treated as 1.0.|
|success	|Function	|否			|接口调用成功的回调函数|						
|success |Function |No |Callback function for successful interface call|
|fail	|Function	|否			|接口调用失败的回调函数|						
|fail |Function |No |Callback function for interface call failure|
|complete	|Function	|否		|接口调用结束的回调函数（调用成功、失败都会执行）		|
|complete |Function |No |Callback function at the end of the interface call (it will be executed if the call succeeds or fails) |

**示例代码**
**Sample Code**

```javascript
uni.canvasToTempFilePath({
  x: 100,
  y: 200,
  width: 50,
  height: 50,
  destWidth: 100,
  destHeight: 100,
  canvasId: 'myCanvas',
  success: function(res) {
    // 在H5平台下，tempFilePath 为 base64
	// Under the H5 platform, tempFilePath is base64
    console.log(res.tempFilePath)
  } 
})
```

**Tips**

- H5端 Canvas 内绘制的图像需要支持跨域访问才能成功。
- Images drawn in Canvas on the H5 end need to support cross-domain access to succeed.