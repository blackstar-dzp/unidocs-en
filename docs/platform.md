## 跨端兼容
## Cross-terminal compatibility

uni-app 已将常用的组件、JS API 封装到框架中，开发者按照 uni-app 规范开发即可保证多平台兼容，大部分业务均可直接满足。
Uni-app has encapsulated commonly used components and JS API into the framework. Developers can ensure multi-platform compatibility by developing in accordance with uni-app specifications, and most businesses can be directly satisfied.

但每个平台有自己的一些特性，因此会存在一些无法跨平台的情况。
But each platform has its own characteristics, so there will be some situations that cannot be cross-platform.

- 大量写 if else，会造成代码执行性能低下和管理混乱。
- Writing a lot of if else will cause poor code execution performance and chaotic management.
- 编译到不同的工程后二次修改，会让后续升级变的很麻烦。
- Second modification after compiling to a different project will make subsequent upgrades very troublesome.

在 C 语言中，通过 #ifdef、#ifndef 的方式，为 windows、mac 等不同 os 编译不同的代码。
In C language, different codes are compiled for different os such as windows and mac through #ifdef and #ifndef.

``uni-app`` 参考这个思路，为 ``uni-app`` 提供了条件编译手段，在一个工程里优雅的完成了平台个性化实现。
``uni-app`` refers to this idea, provides conditional compilation means for ``uni-app``, and elegantly completes the platform personalized realization in a project.


## 条件编译@preprocessor
## Conditional compilation @preprocessor

条件编译是用特殊的注释作为标记，在编译时根据这些特殊的注释，将注释里面的代码编译到不同平台。
Conditional compilation uses special comments as marks. According to these special comments during compilation, the code in the comments is compiled to different platforms.

**写法：**以 <span style="color:#859900;"> #ifdef</span> 或 <span style="color:#859900;"> #ifndef</span> 加<b style="color:#268BD2"> %PLATFORM%</b> 开头，以 <span style="color:#859900;">#endif</span> 结尾。
**How to write: **Add <b style=" with <span style="color:#859900;"> #ifdef</span> or <span style="color:#859900;"> #ifndef</span> color:#268BD2">%PLATFORM%</b> begins and ends with <span style="color:#859900;">#endif</span>.
* <span style="color:#859900;"> #ifdef</span>：if defined 仅在某平台存在
* <span style="color:#859900;"> #ifdef</span>: if defined exists only on a certain platform
* <span style="color:#859900;"> #ifndef</span>：if not defined 除了某平台均存在
* <span style="color:#859900;"> #ifndef</span>: if not defined exists except for a certain platform
* <b style="color:#268BD2"> %PLATFORM%</b>：平台名称
* <b style="color:#268BD2"> %PLATFORM%</b>: platform name
<table>
  <thead>
    <tr>
      <th>条件编译写法</th>
	  <th>Conditional compilation method</th>
      <th>说明</th>
	  <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <div class="code">
          <span class="token comment">
            <span style="color:#859900;">#ifdef</span>
            <b style="color:#268BD2">APP-PLUS</b>
          </span>
          <br>需条件编译的代码<br>
		  <br>Code that requires conditional compilation<br>
          <span class="token comment">
            <span style="color:#859900;">#endif</span></span>
        </div>
      </td>
      <td>仅出现在 App 平台下的代码</td>
	  <td>Code that only appears under the App platform</td>
    </tr>
    <tr>
      <td>
        <div class="code">
          <span class="token comment">
            <span style="color:#859900;">#ifndef</span>
            <b style="color:#268BD2">H5</b>
          </span>
          <br>需条件编译的代码<br>
		  <br>Code that requires conditional compilation<br>
          <span class="token comment">
            <span style="color:#859900;">#endif</span></span>
        </div>
      </td>
      <td>除了 H5 平台，其它平台均存在的代码</td>
	  <td>Except for the H5 platform, codes that exist on other platforms</td>
    </tr>
    <tr>
      <td>
        <div class="code">
          <span class="token comment">
            <span style="color:#859900;">#ifdef</span>
            <b style="color:#268BD2">H5</b>
          </span>
          <span style="color:#859900;">||</span>
          <b style="color:#268BD2">APP-PLUS</b>
          <br>需条件编译的代码<br><span class="token comment"> <span style="color:#859900;">#endif</span></span>
		  <br>Code that requires conditional compilation<br><span class="token comment"> <span style="color:#859900;">#endif</span></span>
		</div>
      </td>
      <td>在 H5 平台或 App 平台存在的代码（这里只有||，不可能出现&&，因为没有交集）</td>
	  <td>Code that exists on the H5 platform or App platform (here there is only ||, && cannot appear because there is no intersection)</td>
    </tr>
  </tbody>
</table>


<b style="color:#268BD2"> %PLATFORM%</b> **可取值如下：**
<b style="color:#268BD2"> %PLATFORM%</b> **The possible values are as follows:**

|值|生效条件|
|Value|Validity Conditions|
|:-|:-|
|VUE3|HBuilderX 3.2.0+ [详情](https://ask.dcloud.net.cn/article/37834)|
|VUE3|HBuilderX 3.2.0+ [details](https://ask.dcloud.net.cn/article/37834)|
|APP-PLUS|App|
|APP-PLUS-NVUE或APP-NVUE|App nvue|
|APP-PLUS-NVUE or APP-NVUE|App nvue|
|H5|H5|


**支持的文件**
**Supported files**

* .vue
* .js
* .css
* pages.json
* 各预编译语言文件，如：.scss、.less、.stylus、.ts、.pug
* All pre-compiled language files, such as: .scss, .less, .stylus, .ts, .pug

**注意：**
**Notice:**

* 条件编译是利用注释实现的，在不同语法里注释写法不一样，js使用 ``// 注释``、css 使用 ``/* 注释 */``、vue/nvue 模板里使用 ``<!-- 注释 -->``；
* Conditional compilation is realized by using comments. The writing of comments in different grammars is different. js uses ``// comments``, css uses ``/* comments*/'', and vue/nvue templates use ``<! - Comment-->``;
* 条件编译APP-PLUS包含APP-NVUE和APP-VUE，APP-PLUS-NVUE和APP-NVUE没什么区别，为了简写后面出了APP-NVUE ；
* Conditional compilation APP-PLUS includes APP-NVUE and APP-VUE, there is no difference between APP-PLUS-NVUE and APP-NVUE, APP-NVUE is listed for abbreviation;
* 使用条件编译请保证`编译前`和`编译后`文件的正确性，比如json文件中不能有多余的逗号；
* When using conditional compilation, please ensure the correctness of the `before compilation` and `after compilation` files, such as no extra commas in the json file;
* `VUE3` 需要在项目的 `manifest.json` 文件根节点配置 `"vueVersion" : "3"`
* `VUE3` needs to configure `"vueVersion": "3"` in the root node of the project's `manifest.json` file

### API 的条件编译
### Conditional compilation of API

<pre v-pre="" data-lang="javascript"><code class="lang-javascript code"><span class="token comment">//<span style="color:#859900;"> #ifdef</span><b style="color:#268BD2">  %PLATFORM%</b></span>
平台特有的API实现
Platform-specific API implementation
<span class="token comment">//<span style="color:#859900;"> #endif</span></span></code></pre>


示例，如下代码仅在 App 下出现:
For example, the following code only appears under App:

![](https://bjetxgzv.cdn.bspapp.com/VKCEYUGU-uni-app-doc/07834e90-4f3c-11eb-b680-7980c8a877b8.png)

示例，如下代码不会在 H5 平台上出现：
For example, the following code will not appear on the H5 platform:

![](https://bjetxgzv.cdn.bspapp.com/VKCEYUGU-uni-app-doc/06a79490-4f3c-11eb-b680-7980c8a877b8.png)

除了支持单个平台的条件编译外，还支持**多平台**同时编译，使用 || 来分隔平台名称。
In addition to supporting conditional compilation of a single platform, it also supports simultaneous compilation of **multi-platforms**, using || to separate platform names.

示例，如下代码会在 App 和 H5 平台上出现：
For example, the following code will appear on the App and H5 platforms:

![](https://bjetxgzv.cdn.bspapp.com/VKCEYUGU-uni-app-doc/05c1ef80-4f3c-11eb-b680-7980c8a877b8.png)

### 组件的条件编译
### Conditional compilation of components
<pre v-pre="" data-lang="html"><code class="lang-html code"><span class="token comment">&lt;!-- <span style="color:#859900;"> #ifdef</span><b style="color:#268BD2">  %PLATFORM%</b> --&gt;</span>
平台特有的组件
Platform-specific components
<span class="token comment">&lt;!-- <span style="color:#859900;"> #endif</span> --&gt;</span></code></pre>

示例，如下组件仅会在App中出现：
For example, the following components will only appear in the App:

````html
<view>
    <view>
        <!-- #ifdef APP-PLUS -->
		        <my-test></my-test>
		    <!-- #endif -->
    </view>
</view>
````

### 样式的条件编译
### Style conditional compilation
<pre v-pre="" data-lang="css"><code class="lang-css code"><span class="token comment">/* <span style="color:#859900;"> #ifdef</span><b style="color:#268BD2">  %PLATFORM% </b> */</span>
平台特有样式
Platform-specific style
<span class="token comment">/* <span style="color:#859900;"> #endif </span> */</span></code></pre>

**注意：** 样式的条件编译，无论是 css 还是 sass/scss/less/stylus 等预编译语言中，必须使用 `/*注释*/` 的写法。
**Note:** For style conditional compilation, whether it is css or precompiled languages such as sass/scss/less/stylus, you must use `/*comment*/`.

正确写法
Correct writing

![](https://bjetxgzv.cdn.bspapp.com/VKCEYUGU-uni-app-doc/0bd78d80-4f3c-11eb-a16f-5b3e54966275.png)

错误写法
Wrong way

![](https://bjetxgzv.cdn.bspapp.com/VKCEYUGU-uni-app-doc/0c9c8b30-4f3c-11eb-8a36-ebb87efcf8c0.png)

### pages.json 的条件编译
### Conditional compilation of pages.json
下面的页面，只有运行至 App 时才会编译进去。
The following page will only be compiled when it runs to the App.

![](https://bjetxgzv.cdn.bspapp.com/VKCEYUGU-uni-app-doc/04ecec40-4f3c-11eb-97b7-0dc4655d6e68.png)

不同平台下的特有功能，都可以通过 pages.json 的条件编译来更好地实现。这样，就不会在其它平台产生多余的资源，进而减小包体积。
The unique functions under different platforms can be better implemented through conditional compilation of pages.json. In this way, redundant resources will not be generated on other platforms, thereby reducing the size of the package.

json的条件编译，如不同平台的key名称相同，cli项目下开发者自己安装的校验器会报错，需自行关闭这些校验器对json相同key的校验规则。如果使用HBuilderX的校验器，无需在意此问题，HBuilderX的语法校验器为此优化过。
Conditional compilation of json, if the key names of different platforms are the same, the verifier installed by the developer under the cli project will report an error, and you need to turn off the verification rules of these verifiers for the same json key. If you use HBuilderX's validator, you don't need to worry about this problem. HBuilderX's syntax validator is optimized for this.

### static 目录的条件编译
### Conditional compilation of static directory
在不同平台，引用的静态资源可能也存在差异，通过 static 的的条件编译可以解决此问题，static 目录下新建不同平台的专有目录（目录名称同 `%PLATFORM%` 值域,但字母均为小写），专有目录下的静态资源只有在特定平台才会编译进去。
On different platforms, the referenced static resources may also be different. This problem can be solved by static conditional compilation. Create a new dedicated directory for different platforms under the static directory (the directory name is the same as the `%PLATFORM%` range, but the letters are all Lowercase), the static resources in the dedicated directory will only be compiled on a specific platform.
如以下目录结构，``a.png`` 只有在 App 平台才会编译进去，``b.png`` 在所有平台都会被编译。
As shown in the following directory structure, ``a.png'' will only be compiled on the App platform, and ``b.png'' will be compiled on all platforms.
<pre v-pre="" data-lang="">
	<code class="lang-" style="padding:0">
┌─static                
│  ├─app-plus
│  │  └─a.png     
│  └─b.png
├─main.js        
├─App.vue      
├─manifest.json 
└─pages.json     
	</code>
</pre>

### 整体目录条件编译
### Overall directory conditional compilation

如果想把各平台的页面文件更彻底的分开，也可以在uni-app项目根目录创建`platforms`目录，然后在下面进一步创建`app-plus`等子目录，存放不同平台的文件。
If you want to separate the page files of each platform more thoroughly, you can also create a `platforms` directory in the root directory of the uni-app project, and then create further subdirectories such as `app-plus` below to store files of different platforms.

**注意**
**Notice**

- `platforms`目录下只支持放置页面文件（即页面vue文件），如果需要对其他资源条件编译建议使用[static 目录的条件编译](https://uniapp.dcloud.io/platform?id=static-%e7%9b%ae%e5%bd%95%e7%9a%84%e6%9d%a1%e4%bb%b6%e7%bc%96%e8%af%91)
- Only page files (ie page vue files) are supported in the `platforms` directory. If you need to compile other resources conditionally, it is recommended to use [conditional compilation in static directory](https://uniapp.dcloud.io/platform?id=static -%e7%9b%ae%e5%bd%95%e7%9a%84%e6%9d%a1%e4%bb%b6%e7%bc%96%e8%af%91)

### HBuilderX 支持
### HBuilderX support
HBuilderX 为 ``uni-app`` 的条件编译提供了丰富的支持:
HBuilderX provides rich support for conditional compilation of ``uni-app``:

**代码块支持**
**Code block support**

在 HBuilderX 中开发 ``uni-app`` 时，通过输入 **ifdef** 可快速生成条件编译的代码片段
When developing ``uni-app`` in HBuilderX, you can quickly generate code fragments for conditional compilation by entering **ifdef**
 
 ![](https://bjetxgzv.cdn.bspapp.com/VKCEYUGU-uni-app-doc/0a1766f0-4f3c-11eb-8a36-ebb87efcf8c0.png)

**语法高亮**
**Syntax highlighting**

在 HBuilderX 中对条件编译的代码注释部分提供了语法高亮，可分辨出写法是否正确，使得代码更加清晰（独立js文件需在编辑器右下角切换javascript es6+编辑器，独立css文件暂不支持高亮，但不高亮不影响使用）
Syntax highlighting is provided for the code comment part of conditional compilation in HBuilderX, which can distinguish whether the writing is correct or not, making the code clearer (independent js files need to switch javascript es6+ editor in the lower right corner of the editor, independent css files do not currently support high Bright, but not highlighting does not affect the use)

![](https://bjetxgzv.cdn.bspapp.com/VKCEYUGU-uni-app-doc/0868a580-4f3c-11eb-8a36-ebb87efcf8c0.png)


**正确注释和快速选中**
**Correct annotation and quick selection**

在 HBuilderX 中，ctrl+alt+/ 即可生成正确注释（js：``// 注释``、css：``/* 注释 */``、vue/nvue模板： ``<!-- 注释 -->``）。
In HBuilderX, ctrl+alt+/ can generate correct comments (js: ``// comment``, css: ``/* comment*/``, vue/nvue template: ``<!-- comment-- >``).

![](https://bjetxgzv.cdn.bspapp.com/VKCEYUGU-uni-app-doc/0af9d7b0-4f3c-11eb-8a36-ebb87efcf8c0.png)

点击 **ifdef** 或 **endif** 可快速选中条件编译部分；点击左侧的折叠图标，可折叠条件编译部分代码。
Click **ifdef** or **endif** to quickly select the conditional compilation part; click the folding icon on the left to collapse part of the conditional compilation code.

![](https://bjetxgzv.cdn.bspapp.com/VKCEYUGU-uni-app-doc/09460d30-4f3c-11eb-8a36-ebb87efcf8c0.png)


### 注意
### Notice
* Android 和 iOS 平台不支持通过条件编译来区分，如果需要区分 Android、iOS 平台，请通过调用 uni.getSystemInfo 来获取平台信息。支持`ifios`、`ifAndroid`代码块，可方便编写判断。
* Android and iOS platforms do not support conditional compilation. If you need to distinguish between Android and iOS platforms, please call uni.getSystemInfo to get platform information. Supports `ifios` and `ifAndroid` code blocks to facilitate writing and judgment.
* 有些跨端工具可以提供js的条件编译或多态，但这对于实际开发远远不够。uni-app不止是处理js，任何代码都可以多端条件编译，才能真正解决实际项目的跨端问题。另外所谓多态在实际开发中会造成大量冗余代码，很不利于复用和维护。
* Some cross-end tools can provide js conditional compilation or polymorphism, but this is far from enough for actual development. Uni-app is not only processing js, any code can be multi-terminal conditional compilation, in order to truly solve the cross-terminal problem of the actual project. In addition, the so-called polymorphism will cause a lot of redundant code in actual development, which is not conducive to reuse and maintenance.
* 有些公司的产品运营总是给不同平台提不同需求，但这不是拒绝uni-app的理由。关键在于项目里，复用的代码多还是个性的代码多，正常都是复用的代码多，所以仍然应该多端。而个性的代码放到不同平台的目录下，差异化维护。
* Some companies' product operations always put different demands on different platforms, but this is not a reason to reject uni-app. The key is that in the project, there are more codes for reuse or more individual codes. Normally, there are more codes for reuse, so it should still be multi-end. The personalized code is placed in the directories of different platforms for differentiated maintenance.