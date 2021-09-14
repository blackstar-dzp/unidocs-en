#### waterfall

app端nvue专用组件。
nvue dedicated component on app side.

`<waterfall>` 组件是提供瀑布流布局的核心组件。瀑布流，又称瀑布流式布局是比较流行的一种页面布局，视觉表现为参差不齐的多栏布局。随着页面滚动条向下滚动，这种布局还可以不断加载数据块并附加至当前尾部。
The `<waterfall>` component is the core component that provides the waterfall flow layout. The waterfall flow, also known as the waterfall flow layout, is a popular page layout, and its visual performance is a jagged multi-column layout. As the page scroll bar scrolls down, this layout can also continuously load data blocks and append them to the current tail.

在nvue中，使用普通view做瀑布流，无法实现重用和不可见渲染资源释放。使用waterfall组件，指定cell后，原生引擎会自动优化性能。
In nvue, using normal views as waterfall flow cannot achieve reuse and release of invisible rendering resources. Using the waterfall component, after specifying the cell, the native engine will automatically optimize the performance.

```
<template>
  <waterfall column-count="2" column-width="auto">
    <cell v-for="num in lists" >
      <text>{{num}}</text>
    </cell>
  </waterfall>
</template>
<script>
  export default {
    data () {
      return {
        lists: ['A', 'B', 'C', 'D', 'E']
      }
    }
  }
</script>

<style></style>
```

#### 子组件
#### Subassembly

和 `<list>` 组件一样, `<waterfall>` 组件的子组件只能包括以下四种组件或是 fix 定位的组件，其他形式的组件将不能被正确渲染。
Like the `<list>` component, the sub-components of the `<waterfall>` component can only include the following four components or fix-positioned components, and other forms of components will not be rendered correctly.

- `<cell>`：用于定义列表中的子列表项，类似于 HTML 中的 ul 之于 li。`<waterfall>` 会对 `<cell>` 进行高效的内存回收以达到更好的性能。
- `<cell>`: Used to define the sub-list items in the list, similar to ul to li in HTML. `<waterfall>` will perform efficient memory recovery on `<cell>` to achieve better performance.
- `<header>`：当 `<header>` 到达屏幕顶部时，吸附在屏幕顶部。
- `<header>`: When `<header>` reaches the top of the screen, it snaps to the top of the screen.
- `<refresh>`：用于给列表添加下拉刷新的功能。
- `<refresh>`: Used to add pull-down refresh function to the list.
- `<loading>`：`<loading>` 用法与特性和 `<refresh>` 类似，用于给列表添加上拉加载更多的功能。
- `<loading>`: The usage and features of `<loading>` are similar to that of `<refresh>`, which is used to add pull-up and load functions to the list.
  <img src="https://bjetxgzv.cdn.bspapp.com/VKCEYUGU-uni-app-doc/e6b5dbe0-4f2e-11eb-97b7-0dc4655d6e68.png" />

#### 属性
#### Attributes

- show-scrollbar : `[可选]` 可选值为 true/ false，默认值为 true。控制是否出现滚动条。
- show-scrollbar: `[Optional]` The optional value is true/false, and the default value is true. Control whether scroll bars appear.
- column-count: `[可选]`描述瀑布流的列数
- column-count: `[optional]` describes the number of columns in the waterfall
  - auto: 意味着列数是被其他属性所决定的(比如 column-width)
  - auto: means that the number of columns is determined by other attributes (such as column-width)
  - `<integer>`: 最佳列数，column-width 和 column-count 都指定非0值， 则 column-count 代表最大列数。
  - `<integer>`: Optimal number of columns. Both column-width and column-count specify non-zero values, then column-count represents the maximum number of columns.
- column-width : `[可选]`描述瀑布流每一列的列宽
- column-width: `[optional]` describes the column width of each column of the waterfall
  - `auto`: 意味着列宽是被其他属性所决定的(比如 column-count)
  - `auto`: means that the column width is determined by other attributes (such as column-count)
  - `<length>`: 最佳列宽，实际的列宽可能会更宽(需要填充剩余的空间)， 或者更窄(如果剩余空间比列宽还要小)。 该值必须大于0
  - `<length>`: The best column width, the actual column width may be wider (the remaining space needs to be filled), or narrower (if the remaining space is smaller than the column width). The value must be greater than 0
- column-gap: [可选]列与列的间隙. 如果指定了 `normal` ，则对应 32.
- column-gap: [Optional] The gap between the column and the column. If `normal` is specified, it corresponds to 32.
- left-gap: [可选]左边cell和列表的间隙. 如果未指定 ，则对应 `0`
- left-gap: [Optional] The gap between the left cell and the list. If not specified, it corresponds to `0`
- right-gap: [可选]右边cell和列表的间隙. 如果未指定，则对应 `0`
- right-gap: [optional] The gap between the right cell and the list. If not specified, it corresponds to `0`
  <img src="https://bjetxgzv.cdn.bspapp.com/VKCEYUGU-uni-app-doc/e78b5450-4f2e-11eb-b680-7980c8a877b8.png" />

其他支持的属性参见 `<list>` 组件属性部分
See the `<list>` component properties section for other supported properties

#### 事件
#### event
支持所有通用事件：
Support all common events:

- click：用于监听点击事件。（例如：一般绑定于子组件之上触发跳转）。
- click: used to monitor click events. (For example: it is generally bound to a sub-component to trigger a jump).
- longpress：用于监听长按事件（一般绑定于子组件之上例如：长按可删除）。
- longpress: used to monitor long press events (usually bound to sub-components, for example: long press to delete).
- appear：用于监听子组件出现事件（一般绑定于子组件之上例如：监听最后一个元素出现，加载新的数据）
- Appear: Used to monitor the appearance of sub-components (generally bound to the sub-components, for example: monitor the appearance of the last element, load new data)
- disappear：用于监听子组件滑出屏幕事件（一般绑定于子组件之上）
- disappear: used to monitor the event of the child component sliding out of the screen (generally bound to the child component)

**注意**
**Notice**
- waterfall是区域滚动，不会触发页面滚动，无法触发pages.json配置的下拉刷新、页面触底onReachBottomDistance、titleNView的transparent透明渐变。
- Waterfall is area scrolling and will not trigger page scrolling. It cannot trigger the pull-down refresh configured in pages.json, the page bottoming onReachBottomDistance, and the transparent gradient of titleNView.