### uni.getLocation(OBJECT)
获取当前的地理位置、速度。
Get the current geographic location and speed.


**OBJECT 参数说明**
**OBJECT parameter description**

|参数名|类型|必填|说明|平台差异说明|
| parameter name | Types    | Required | Description     |Platform difference description|
|:-|:-|:-|:-|:-:|
|type|String|否|默认为 wgs84 返回 gps 坐标，gcj02 返回国测局坐标，可用于 ``uni.openLocation`` 的坐标，app平台高德SDK仅支持返回gcj02||
| type           | String   | no       | The default is wgs84 return gps coordinates, gcj02 return to the country office coordinate measurement can be used to `uni.openLocation`coordinate, app platform high moral SDK only supports returning gcj02 ||
|altitude|Boolean|否|传入 true 会返回高度信息，由于获取高度需要较高精确度，会减慢接口返回速度|App不支持|
|altitude|Boolean|No|Passing true will return altitude information. Because obtaining altitude requires high accuracy, it will slow down the interface return speed|App does not support|
|geocode|Boolean|否|默认false，是否解析地址信息|仅App平台支持|
|geocode|Boolean|否|Default value false, whether to resolve address information|Only supported `App` platform|
|success|Function|是|接口调用成功的回调函数，返回内容详见返回参数说明。||
| success        | Function | Yes      | Callback function for successful interface call. For details, see the return parameter description. ||
|fail|Function|否|接口调用失败的回调函数||
| fail           | Function | no       | Callback function for interface call failure                 ||
|complete|Function|否|接口调用结束的回调函数（调用成功、失败都会执行）|&nbsp;|
| complete       | Function | no       | The callback function for the end of the interface call (the call will be executed if it succeeds or fails) ||

**success 返回参数说明**
**success return parameter description**

|参数|说明|
|Parameters|Description|
|:-|:-|
|latitude|纬度，浮点数，范围为-90~90，负数表示南纬|
| latitude           | Latitude, floating point number, range -90~90, negative number means south latitude |
|longitude|经度，浮点数，范围为-180~180，负数表示西经|
| longitude          | Longitude, floating point number, range -180~180, negative number means west longitude |
|speed|速度，浮点数，单位m/s|
| speed              | Speed, floating point number, unit m/s |
|accuracy|位置的精确度|
| accuracy           | Position accuracy    |
|altitude|高度，单位 m|
| altitude           | Height, unit m   |
|verticalAccuracy|垂直精度，单位 m（Android 无法获取，返回 0）|
| verticalAccuracy   | Vertical accuracy, unit m (Android can’t get it, return 0)   |
|horizontalAccuracy|水平精度，单位 m|
| horizontalAccuracy | Horizontal accuracy, unit m   |
|[address](/api/location/location?id=address)|地址信息（仅App端支持，需配置geocode为true）|
|[address](/api/location/location?id=address)|Address information (Only supported `App` platform, Need to configure geocode to true)|

**address 地址信息说明**
**address information description**

|属性|类型|描述|说明|
| Attributes | Types  | description                   | Description     |
|:-|:-|:-|:-|
|country|String|国家|如“中国”，如果无法获取此信息则返回undefined|
| country    | String | country                       | Such as "China", if this information cannot be obtained, undefined will be returned |
|province|String|省份名称|如“北京市”，如果无法获取此信息则返回undefined|
| province   | String | Province name                 | Such as "Beijing", if the information cannot be obtained, undefined will be returned |
|city|String|城市名称|如“北京市”，如果无法获取此信息则返回undefined|
| city       | String | city name                     | Such as "Beijing", if the information cannot be obtained, undefined will be returned |
|district|String|区（县）名称|如“朝阳区”，如果无法获取此信息则返回undefined|
| district   | String | District (county) name        | Such as "Chaoyang District", if this information cannot be obtained, undefined will be returned |
|street|String|街道信息|如“酒仙桥路”，如果无法获取此信息则返回undefined|
| street     | String | Street information            | Such as "Jiuxianqiao Road", if this information cannot be obtained, undefined will be returned |
|streetNum|String|获取街道门牌号信息|如“3号”，如果无法获取此信息则返回undefined|
| streetNum  | String | Get street number information | Such as "No. 3", if this information cannot be obtained, undefined will be returned |
|poiName|String|POI信息|如“电子城．国际电子总部”，如果无法获取此信息则返回undefined|
| poiName    | String | POI information               | Such as "Electronic City. International Electronic Headquarters", if this information cannot be obtained, undefined will be returned |
|postalCode|String|邮政编码|如“100016”，如果无法获取此信息则返回undefined|
| postalCode | String | Postal code                   | Such as "100016", if this information cannot be obtained, undefined will be returned |
|cityCode|String|城市代码|如“010”，如果无法获取此信息则返回undefined|
| cityCode   | String | City code                     | Such as "010", if this information cannot be obtained, undefined will be returned |

**示例**
**Example**

```javascript
uni.getLocation({
	type: 'wgs84',
	success: function (res) {
		console.log('当前位置的经度：' + res.longitude);
		console.log('The longitude of the current position:' + res.longitude);
		console.log('当前位置的纬度：' + res.latitude);
		console.log('The latitude of the current position:' + res.latitude);
	}
});
```

#### 注意
#### Notice

- H5：在较新的浏览器上，H5 端获取定位信息，要求部署在 **https** 服务上，本地预览（localhost）仍然可以使用 http 协议。
- H5: On newer browsers, the H5 terminal obtains location information and requires deployment on the **https** service. The local preview (localhost) can still use the http protocol.
- H5：国产安卓手机上，H5若无法定位，检查手机是否开通位置服务、GPS，ROM是否给该浏览器位置权限、浏览器是否对网页弹出请求给予定位的询问框。
- H5: On domestic Android phones, if H5 cannot be located, check whether the mobile phone has location service, GPS, whether the ROM gives the browser location permission, and whether the browser pops up a request box for positioning on the web page.
- H5：安卓手机在原生App内嵌H5时，无法定位需要原生App处理Webview。
- H5: When the Android phone has H5 embedded in the native App, it cannot be located and requires the native App to process the Webview.
- H5：移动端浏览器普遍仅支持GPS定位，在GPS信号弱的地方可能定位失败。
- H5: Mobile browsers generally only support GPS positioning, and positioning may fail in places with weak GPS signals.
- H5：PC 设备使用 Chrome 浏览器的时候，位置信息是连接谷歌服务器获取的，国内用户可能获取位置信息失败。
- H5: When the PC device uses the Chrome browser, the location information is obtained by connecting to the Google server, and domestic users may fail to obtain the location information.
- H5：使用地图和定位相关需要在[腾讯地图开放平台](https://lbs.qq.com/dev/console/key/manage)申请密钥，填写在 [manifest.json](https://uniapp.dcloud.io/collocation/manifest?id=h5sdkconfig) 中。
- H5: To use maps and positioning, you need to apply for a key in [Tencent Maps Open Platform](https://lbs.qq.com/dev/console/key/manage), and fill in [manifest.json](https:/ /uniapp.dcloud.io/collocation/manifest?id=h5sdkconfig).
- H5：2.9.9 alpha升级，优化 uni.getLocation 支持通过 IP 定位。默认通过getLocation获取，如果获取失败，备选方案是通过 IP 定位获取，用的是内置公共的key，如果你想正确使用，就填写正常的key。如果你不想使用，就填写错误的key即可。key配置：manifest.json ---> H5配置 ---> 定位和地图 ---> key。
- H5: 2.9.9 alpha upgrade, optimization uni.getLocation supports positioning via IP. The default is to obtain it through getLocation. If the acquisition fails, the alternative is to obtain it through IP location, using the built-in public key. If you want to use it correctly, fill in the normal key. If you don't want to use it, just fill in the wrong key. Key configuration: manifest.json ---> H5 configuration ---> location and map ---> key.
- App：Android由于谷歌服务被墙，或者手机上没有GMS，想正常定位就需要向高德等三方服务商申请SDK资质，获取AppKey。否则打包后定位就会不准。云打包时需要在manifest的SDK配置中填写Appkey。在manifest可视化界面有详细申请指南，详见：[https://ask.dcloud.net.cn/article/29](https://ask.dcloud.net.cn/article/29)。离线打包自行在原生工程中配置。注意包名、appkey、证书信息必须匹配。真机运行可以正常定位，是因为真机运行基座使用了DCloud向高德申请的sdk配置，打包后必须由开发者自己申请。如果手机自带GMS且网络环境可以正常访问google定位服务器，此时无需在manifest填写高德定位的sdk配置。
- App: For Android, because Google services are blocked, or there is no GMS on the phone, you need to apply for SDK qualifications from third-party service providers such as AutoNavi, and obtain AppKey for normal positioning. Otherwise, the positioning will be inaccurate after packaging. When cloud packaging, you need to fill in Appkey in the SDK configuration of the manifest. There is a detailed application guide in the manifest visualization interface, see: [https://ask.dcloud.net.cn/article/29](https://ask.dcloud.net.cn/article/29). Offline packaging is configured in the native project by itself. Note that the package name, appkey, and certificate information must match. The real machine operation can be positioned normally because the real machine operation base uses the SDK configuration that DCloud applied to AutoNavi, and the developer must apply for it after packaging. If the mobile phone comes with GMS and the network environment can access the Google location server normally, there is no need to fill in the SDK configuration of AutoNavi in ​​the manifest at this time.
- App：``<map>`` 组件默认为国测局坐标gcj02，调用 ``uni.getLocation`` 返回结果传递给 ``<map>`` 组件时，需指定 type 为 gcj02。
- App: The ``<map>`` component defaults to the coordinate gcj02 of the National Bureau of Survey and Measurement. When calling ``uni.getLocation`` to return the result to the ``<map>`` component, you need to specify the type as gcj02.
- App：定位和map是2个东西。通过`getLocation`得到位置坐标后，可以在任意map地图上展示，比如定位使用高德，地图使用google的webview版地图。如果坐标系不同时，注意转换坐标系。
- App: Location and map are two things. After getting the location coordinates through `getLocation`, they can be displayed on any map map, such as using AutoNavi for positioning, and using Google's webview version of the map for the map. If the coordinate system is different, pay attention to converting the coordinate system.
- App：如果使用web-view加载地图，无需在manifest里配地图的sdk配置。
- App: If you use web-view to load the map, you don't need to configure the sdk configuration of the map in the manifest.
- App：持续定位方案：iOS端可以申请持续定位权限，[参考](https://ask.dcloud.net.cn/article/12569)。Android如果进程被杀，代码无法执行。可以使用[unipush](https://ask.dcloud.net.cn/article/35622)，通过服务器激活App，执行透传消息，让App启动然后采集位置。Android上，即使自己写原生插件做后台进程，也很容易被杀，unipush是更合适的方案
- App: Continuous positioning solution: iOS can apply for continuous positioning permission, [Reference](https://ask.dcloud.net.cn/article/12569). If the Android process is killed, the code cannot be executed. You can use [unipush](https://ask.dcloud.net.cn/article/35622) to activate the App through the server, execute the transparent message, let the App start and then collect the location. On Android, even if you write a native plug-in as a background process, it is easy to be killed. Unipush is a more suitable solution.
- 可以通过用户授权API来判断用户是否给应用授予定位权限[https://uniapp.dcloud.io/api/other/authorize](https://uniapp.dcloud.io/api/other/authorize)
- The user authorization API can be used to determine whether the user has granted location permissions to the application [https://uniapp.dcloud.io/api/other/authorize](https://uniapp.dcloud.io/api/other/authorize)

### uni.chooseLocation(OBJECT)
打开地图选择位置。
Open the map and select a location.

**平台差异说明**
**Platform difference description**

|App|H5|
|:-:|:-:|
|√|√|


**OBJECT 参数说明**
**OBJECT parameter description**

|参数名|类型|必填|说明|
| parameter name | Type | Required | Description    |
|:-|:-|:-|:-|
|keyword|String|否|搜索关键字，仅App平台支持|
|keyword|String|no|Search keywords, only supported by App platform|
|success|Function|是|接口调用成功的回调函数，返回内容详见返回参数说明。|
| success        | Function | Yes      | Callback function for successful interface call. For details, see the return parameter description. |
|fail|Function|否|接口调用失败的回调函数（获取定位失败、用户取消等情况下触发）|
| fail           | Function | no       | Callback function for interface call failure (triggered when the location fails to obtain, the user cancels, etc.) |
|complete|Function|否|接口调用结束的回调函数（调用成功、失败都会执行）|
| complete       | Function | no       | The callback function for the end of the interface call (the call will be executed if it succeeds or fails) |

**注意**
**Notice**
- 因平台差异，如果SDK配置百度地图，需要设置keyword，才能显示相关地点
- Due to platform differences, if the SDK is configured with Baidu Maps, the keyword needs to be set to display the relevant locations
- nvue下只支持高德地图，不支持百度地图
- Only Gaode maps are supported under nvue, but Baidu maps are not supported
- HBuilderX 2.4.0+ 非 weex 编译模式仅支持高德地图
- HBuilderX 2.4.0+ non-weex compilation mode only supports AutoNavi map

**success 返回参数说明**
**success return parameter description**

|参数|说明|
|Parameters|Description|
|:-|:-|
|name|位置名称|
|name|Location name|
|address|详细地址|
|address|Detailed address|
|latitude|纬度，浮点数，范围为-90~90，负数表示南纬，使用 gcj02 国测局坐标系。|
|latitude|Latitude, floating point number, range -90~90, negative number means south latitude, use gcj02 China National Surveying Bureau coordinate system.|
|longitude|经度，浮点数，范围为-180~180，负数表示西经，使用 gcj02 国测局坐标系。|
|longitude|Longitude, floating point number, range -180~180, negative number means west longitude, use gcj02 China National Surveying Bureau coordinate system.|

**示例**
**Example**

```javascript
uni.chooseLocation({
	success: function (res) {
		console.log('位置名称：' + res.name);
		console.log('Location name:' + res.name);
		console.log('详细地址：' + res.address);
		console.log('Detailed address:' + res.address);
		console.log('纬度：' + res.latitude);
		console.log('Latitude:' + res.latitude);
		console.log('经度：' + res.longitude);
		console.log('longitude:' + res.longitude);
	}
});
```

**注意**
**Notice**
- 不同端，使用地图选择时基于的底层地图引擎不一样，如H5是腾讯地图，App是高德地图，详见地图map组件的使用注意事项。
- For different terminals, the underlying map engine used for map selection is different. For example, H5 is a Tencent map, and the App is a Gaode map. For details, please refer to the precautions for the use of the map component.
- app中也可以使用百度定位，在manifest中配置，打包后生效。但app-nvue里只能用高德定位，不能用百度地图。另外选择地图、查看地图位置的API也仅支持高德地图。所以App端如无特殊必要，建议使用高德地图。
- Baidu positioning can also be used in the app, configured in the manifest, and it will take effect after packaging. But in app-nvue, you can only use AutoNavi for positioning, not Baidu map. In addition, the API for selecting maps and viewing map locations also only supports Gaode maps. Therefore, if there is no special need on the App side, it is recommended to use Gaode map.
- chooseLocation属于封装型API，开发者若觉得不够灵活，可自行基于原始的map组件进行封装。插件市场已经有各种封装样例了。
- chooseLocation is an encapsulated API. If developers feel that it is not flexible enough, they can encapsulate it based on the original map component. There are already various package examples in the plug-in market.
- 若Android App端位置不准，见上文uni.getLocation的注意事项
- If the location of the Android App is inaccurate, please refer to the precautions of uni.getLocation above