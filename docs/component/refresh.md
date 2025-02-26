#### refresh

app端nvue专用组件。
nvue dedicated component on app side.

`<refresh>` 为容器提供下拉刷新功能。在nvue上，可通过此组件实现灵活的、自定义的、高性能的下拉刷新。
`<refresh>` Provides a pull-down refresh function for the container. On nvue, flexible, custom, high-performance pull-down refresh can be realized through this component.

> 注意
> Attention
> - `<refresh>` 是 `<scroll-view>`、`<list>`、`<waterfall>` 的子组件，只能在被它们包含时才能被正确渲染。
> - `<refresh>` is a child component of `<scroll-view>`, `<list>`, and `<waterfall>`, and can only be rendered correctly when they are included.






```
<scroll-view>
  <refresh>
    <text>Refreshing...</text>
  </refresh>
  <view v-for="num in lists">
    <text>{{num}}</text>
  </view>
</scroll-view>
```

#### 子组件
#### Subassembly

- 诸如 `<text>`、`<image>` 之类的任何组件，都可以放到 `<loading>` 进行渲染。
- Any component such as `<text>`, `<image>`, etc., can be placed in `<loading>` for rendering.
- 特殊子组件 `<loading-indicator>`: 只能作为 `<refresh>` 和 `<loading>` 的子组件使用，拥有默认的动画效果实现。
- Special sub-component `<loading-indicator>`: It can only be used as a sub-component of `<refresh>` and `<loading>`, with default animation effect implementation.

```
<refresh>
  <text>Refreshing</text>
  <loading-indicator></loading-indicator>
</refresh>
```

#### 属性
#### Attributes

`display`
`display`
控制 `<refresh>` 组件显示、隐藏。`display` 的设置必须成对出现，即设置 `display="show"`, 必须有对应的 `display="hide"`。可选值为 `show / hide`，默认值为 `show`。
Control the display and hide of the `<refresh>` component. The setting of `display` must appear in pairs, that is, setting `display="show"`, there must be a corresponding `display="hide"`. Optional values are `show / hide`, and the default value is `show`.

#### 事件
#### event
- refresh 事件：当 `<scroll-view>`、`<list>`、`<waterfall>` 被下拉完成时触发。
- -refresh event: triggered when `<scroll-view>`, `<list>`, `<waterfall>` are pulled down to complete.
- pullingdown 事件：当 `<scroll-view>`、`<list>`、`<waterfall>` 被下拉时触发。 可以从 `event` 参数对象中获取以下数据：
- -pullingdown event: triggered when `<scroll-view>`, `<list>`, `<waterfall>` are pulled down. The following data can be obtained from the `event` parameter object:
  - `dy`: 前后两次回调滑动距离的差值
  - `dy`: The difference between the sliding distance of the two callbacks before and after
  - `pullingDistance`: 下拉的距离
  - `pullingDistance`: pull-down distance
  - `viewHeight`: refresh 组件高度
  - `viewHeight`: refresh component height
  - `type`: “pullingdown” 常数字符串
  - `type`: "pullingdown" constant string

```
<refresh @refresh="onrefresh" @pullingdown="onpullingdown" :display="refreshing ? 'show' : 'hide'">
  <text>Refreshing ...</text>
  <loading-indicator></loading-indicator>
</refresh>
```
