#### navigation-bar

页面导航条配置节点，用于指定导航栏的一些属性。只能是 [page-meta](https://uniapp.dcloud.io/component/page-meta) 组件内的第一个节点，需要配合它一同使用。
The page navigation bar configuration node is used to specify some properties of the navigation bar. It can only be the first node in the page-meta component, and it needs to be used together.

**平台差异说明**
**Platform difference description**

|App|H5|
|:-:|:-:|
|√ 2.6.7+|2.6.3+|

从HBuilderX 2.9.3起，编译到所有平台均支持`navigation-bar`，但编译到微信时，受微信基础库版本限制；编译到其他平台不受平台版本限制。
Starting from HBuilderX 2.9.3, all platforms support `navigation-bar` when compiled to WeChat, but when compiled to WeChat, it is limited by the WeChat base library version; when compiled to other platforms, it is not restricted by the platform version.

**属性说明**
**Property description**

|属性|类型|默认值|必填|说明|
| Attributes        | Types of | Defaults           | Required | Description                                                  |
|:-|:-|:-|:-|:-|
|title-icon|string||否|标题图标，图标路径如"./img/t.png"，仅支持本地文件路径， 相对路径，相对于当前页面的host位置，固定宽高为逻辑像素值"34px"。 要求图片的宽高相同。 注意：设置标题图标后标题将居左显示。|
| title-icon        | string   |                    | no       | Title icon, icon path such as "./img/t.png", only supports local file path, relative path, relative to the host position of the current page, fixed width and height are logical pixel value "34px". The width and height of the pictures must be the same. Note: The title will be displayed on the left after setting the title icon. |
|title-icon-radius|string|无圆角|否|标题图标圆角，取值格式为"XXpx"，其中XX为像素值（逻辑像素），如"10px"表示10像素半径圆角。|
| title-icon-radius | string   | No rounded corners | no       | The rounded corners of the title icon, the value format is "XXpx", where XX is the pixel value (logical pixels), for example, "10px" means a 10-pixel radius rounded corner. |
|subtitle-text|string||否|副标题文字内容，设置副标后将显示两行标题，副标显示在主标题（titleText）下方。 注意：设置副标题后将居左显示|
| subtitle-text     | string   |                    | no       | Subtitle text content. After setting the subtitle, two lines of title will be displayed, and the subtitle will be displayed below the main title (titleText). Note: After setting the subtitle, it will be displayed on the left |
|subtitle-size|string|"auto"|否|副标题文字字体大小，字体大小单位为像素，如"14px"表示字体大小为14像素，默认值为12像素。|
| subtitle-size     | string   | "auto"             | no       | The font size of the subtitle text. The font size unit is pixels. For example, "14px" means the font size is 14 pixels, and the default value is 12 pixels. |
|subtitle-color|string||否|副标题文字颜色，颜色值格式为"#RRGGBB"和"rgba(R,G,B,A)"，如"#FF0000"表示标题文字颜色为红色。 默认值与主标题文字颜色一致|
| subtitle-color    | string   |                    | no       | The color of the subtitle text. The color value format is "#RRGGBB" and "rgba(R,G,B,A)". For example, "#FF0000" means that the title text color is red. The default value is the same as the main title text color |
|subtitle-overflow|string|"ellipsis"|否|标题文字超出显示区域时处理方式，可取值： "clip" - 超出显示区域时内容裁剪； "ellipsis" - 超出显示区域时尾部显示省略标记（...）。|
| subtitle-overflow | string   | "ellipsis"         | no       | The processing method when the title text exceeds the display area, the possible values are: "clip"-the content is clipped when it exceeds the display area; "ellipsis"-an ellipsis (...) is displayed at the end when it exceeds the display area. |
|title-align|string|"auto"|否|可取值： "center"-居中对齐； "left"-居左对齐； "auto"-根据平台自动选择（Android平台居左对齐，iOS平台居中对齐）|
| title-align       | string   | "auto"             | no       | Possible values: "center"-align to the center; "left"-align to the left; "auto"-automatically select according to the platform (left-aligned on Android platform, center-aligned on iOS platform) |
|background-image|string||否|支持以下类型： 背景图片路径 - 如"./img/t.png"，仅支持本地文件路径， 相对路径，相对于当前页面的host位置，根据实际标题栏宽高拉伸绘制； 渐变色 - 仅支持线性渐变，两种颜色的渐变，如“linear-gradient(to top, #a80077, #66ff00)”， 其中第一个参数为渐变方向，可取值： "to right"表示从左向右渐变， “to left"表示从右向左渐变， “to bottom"表示从上到下渐变， “to top"表示从下到上渐变， “to bottom right"表示从左上角到右下角， “to top left"表示从右下角到左上角|
| background-image  | string   |                    | no       | The following types are supported: Background image path-such as "./img/t.png", only supports local file path, relative path, relative to the host location of the current page, drawn according to the actual title bar width and height; gradient color-only Support linear gradient, two-color gradient, such as "linear-gradient(to top, #a80077, #66ff00)", where the first parameter is the direction of the gradient, which can be a value: "to right" means gradient from left to right , "To left" means gradient from right to left, "to bottom" means gradient from top to bottom, "to top" means gradient from bottom to top, "to bottom right" means from upper left corner to lower right corner, "to top" "left" means from the lower right corner to the upper left corner |
|background-repeat|string||否|仅在backgroundImage设置为图片路径时有效。 可取值： "repeat" - 背景图片在垂直方向和水平方向平铺； "repeat-x" - 背景图片在水平方向平铺，垂直方向拉伸； “repeat-y” - 背景图片在垂直方向平铺，水平方向拉伸； “no-repeat” - 背景图片在垂直方向和水平方向都拉伸。 默认使用 “no-repeat"|
| background-repeat | string   |                    | no       | Only valid when backgroundImage is set to the image path. Possible values: "repeat"-the background image is tiled vertically and horizontally; "repeat-x"-the background image is tiled horizontally and stretched vertically; "repeat-y"-the background image is tiled vertically Shop, stretch horizontally; "no-repeat"-the background image stretches both vertically and horizontally. "No-repeat" is used by default |
|blur-effect|string|"none"|否|此效果将会高斯模糊显示标题栏后的内容，仅在type为"transparent"或"float"时有效。 可取值： "dark" - 暗风格模糊，对应iOS原生UIBlurEffectStyleDark效果； "extralight" - 高亮风格模糊，对应iOS原生UIBlurEffectStyleExtraLight效果； "light" - 亮风格模糊，对应iOS原生UIBlurEffectStyleLight效果； "none" - 无模糊效果。 注意：使用模糊效果时应避免设置背景颜色，设置背景颜色可能覆盖模糊效果。|
| blur-effect       | string   | "none"             | no       | This effect will display the content behind the title bar in a Gaussian blur. It is only effective when the type is "transparent" or "float". Possible values: "dark"-dark style blur, corresponding to iOS native UIBlurEffectStyleDark effect; "extralight"-highlight style blur, corresponding to iOS native UIBlurEffectStyleExtraLight effect; "light"-bright style blur, corresponding to iOS native UIBlurEffectStyleLight effect; "none" -No blur effect. Note: Avoid setting the background color when using the blur effect. Setting the background color may cover the blur effect. |


属性说明 [/collocation/pages?id=app-titlenview](/collocation/pages?id=app-titlenview)
Attribute description [/collocation/pages?id=app-titlenview](/collocation/pages?id=app-titlenview)

**注意**
**note**
- `navigation-bar` 目前支持的配置仅为上表所列，并不支持 page.json 中关于导航栏的所有配置
- `navigation-bar` The currently supported configurations are only listed in the above table, and all the configurations of the navigation bar in page.json are not supported
- `navigation-bar` 与 pages.json 的设置相冲突时，会覆盖 page.json 的配置
- `navigation-bar` When it conflicts with the settings of pages.json, the settings of page.json will be overwritten


#### 示例代码
#### Exemple code

```html
<template>
  <page-meta>
    <navigation-bar
      :title="nbTitle"
      :title-icon="titleIcon"
      :title-icon-radius="titleIconRadius"
      :subtitle-text="subtitleText"
      :subtitle-color="nbFrontColor"
      :loading="nbLoading"
      :front-color="nbFrontColor"
      :background-color="nbBackgroundColor"
      :color-animation-duration="2000"
      color-animation-timing-func="easeIn"
    />
  </page-meta>
  <view class="content"></view>
</template>

<script>
  export default {
    data() {
      return {
        nbTitle: 'Title',
        titleIcon: '/static/logo.png',
        titleIconRadius: '20px',
        subtitleText: 'subtitleText',
        nbLoading: false,
        nbFrontColor: '#000000',
        nbBackgroundColor: '#ffffff'
      }
    },
    onLoad() {
    },
    methods: {
    }
  }
</script>
```
