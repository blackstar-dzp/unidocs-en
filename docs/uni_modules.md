# uni_modules

### 什么是 uni_modules
### What is uni_modules

`uni_modules`是uni-app的插件模块化规范（HBuilderX 3.1.0+支持），通常是对一组js sdk、组件、页面、uniCloud云函数、公共模块等的封装，用于嵌入到uni-app项目中使用，也支持直接封装为项目模板。
`uni_modules` is the plug-in modular specification of uni-app (supported by HBuilderX 3.1.0+), usually a package of js sdk, components, pages, uniCloud cloud functions, public modules, etc., for embedding into uni-app Used in the project, it also supports direct packaging as a project template.

插件开发者，可以像开发uni-app项目一样编写一个`uni_modules`插件，并在HBuilderX中直接上传至[插件市场](https://ext.dcloud.net.cn/)。
Plug-in developers can write a `uni_modules` plugin just like developing uni-app projects, and upload it directly to [plugin market](https://ext.dcloud.net.cn/) in HBuilderX.

插件使用者，可以在[插件市场](https://ext.dcloud.net.cn/)查找符合自己需求的`uni_modules`插件，使用HBuilderX 3.1.0+直接导入到自己的uni-app项目中。后续还可以在HBuilderX中直接点右键升级插件。
Plug-in users can find the `uni_modules` plugin that meets their needs in [Plugin Market](https://ext.dcloud.net.cn/), and use HBuilderX 3.1.0+ to import directly into their uni-app project . You can also right-click to upgrade the plug-in in HBuilderX later.

相对于普通的插件，`uni_modules`插件拥有更强的独立性，拥有独立的目录结构，可以更加方便的发布，更新，卸载（HBuilderX 3.1.0+对`uni_modules`插件提供了右键菜单，支持发布，更新，安装依赖等）
Compared with ordinary plug-ins, the `uni_modules` plug-in has stronger independence, has an independent directory structure, and can be released, updated, and uninstalled more conveniently (HBuilderX 3.1.0+ provides a right-click menu for the `uni_modules` plug-in to support publishing , Update, install dependencies, etc.)

相对于node_modules（node.js模块），`uni_modules`的三方依赖安装时默认最新版本，插件均直接安装在`uni_modules`目录下，不做嵌套，当然，如果开发者希望固定某个版本的依赖，可以将该三方依赖包含到自己的插件包内。
Compared with node_modules (node.js module), the third-party dependency of `uni_modules` defaults to the latest version when installed. Plug-ins are installed directly in the `uni_modules` directory without nesting. Of course, if the developer wants to fix a certain version of the dependency , You can include this third-party dependency into your own plug-in package.

为什么有了`node_modules`，还需要再发明一个`uni_modules`的轮子？
Why is there a need to invent a wheel of `uni_modules` with `node_modules`?
1. `node_modules` 不满足云端一体的需求。uniCloud的云函数、公共模块、schema和前端的各种js_sdk、组件、页面、项目，无法在`node_modules`模式下有效融合。
1. `node_modules` does not meet the requirements of cloud integration. UniCloud cloud functions, public modules, schemas, and various js_sdk, components, pages, and projects in the front end cannot be effectively integrated in the `node_modules` mode.
2. `uni_modules`有付费和商业的插件，DCloud插件市场提供了版权保护。而`node_modules`不支持付费和版权保护。
2. There are paid and commercial plug-ins for `uni_modules`, and the DCloud plug-in market provides copyright protection. And `node_modules` does not support payment and copyright protection.
3. `node_modules` 是开发者友好而影响终端用户性能的模式。开发者为了省事，层层嵌套`node_modules`，造成数量惊人的文件数目。`uni_modules`不支持module嵌套，鼓励开发者优化包体积
3. `node_modules` is a developer-friendly mode that affects end-user performance. In order to save trouble, developers nest `node_modules` layer by layer, resulting in an astonishing number of files. `uni_modules` does not support module nesting, developers are encouraged to optimize the package size
4. `uni_modules`鼓励开发者总是使用最新版。并在HBuilderX中提供了版本内容对比工具
4. `uni_modules` encourages developers to always use the latest version. And provides a version content comparison tool in HBuilderX
5. `uni_modules`里也支持放置`node_modules`，没有强行排斥。
5. `node_modules` is also supported in `uni_modules`, there is no forced rejection.
与之前插件市场的普通插件相比，`uni_modules`有何优势？
Compared with ordinary plugins in the plugin market, what are the advantages of `uni_modules`?
1. 支持在HBuilderX里直接发布、更新、删除
1. Support for publishing, updating, and deleting directly in HBuilderX
2. 支持依赖（在package.json中配置）
2. Support dependencies (configured in package.json)
3. 插件文件位置统一，不会造成下载一个插件，不知道给工程下多少个目录写入了多少个文件。删除插件时也可以一点删除
3. The location of the plug-in files is uniform, which will not cause a plug-in to be downloaded. I don't know how many files are written into the directories under the project. You can also delete a little bit when deleting the plug-in


### 目录结构
### Directory Structure

`uni_modules`插件如果是项目类型的插件，只需要在项目的根目录下放一个符合`uni_modules`规范的package.json。
If the `uni_modules` plugin is a project type plugin, you only need to put a package.json that conforms to the `uni_modules` specification in the root directory of the project.

如果是非项目类型的插件，比如组件、js sdk、页面模板、云函数，则需要放置在项目的`uni_modules`目录下。
If it is a non-project type plug-in, such as component, js sdk, page template, cloud function, it needs to be placed in the `uni_modules` directory of the project.

此时`uni_modules`目录下的目录结构和uni-app的项目结构是一致的，如下：
At this time, the directory structure under the `uni_modules` directory is consistent with the uni-app project structure, as follows:
<pre v-pre="" data-lang="">
	<code class="lang-" style="padding:0">
uni_modules                                项目根目录下(Project root directory)
└── [plugin_id] // 插件 ID(Plugin ID)
    ├── uniCloud                           插件内的uniCloud内容会被虚拟合并到项目根目录的uniCloud中（注意：插件内的uniCloud目录，没有-aliyun,-tcb后缀）(The uniCloud content in the plug-in will be virtually merged into uniCloud in the project root directory (note: the uniCloud directory in the plug-in does not have -aliyun, -tcb suffixes))
    ├── components                         符合vue组件规范的uni-app组件目录，支持easycom规范(Uni-app component catalog that complies with vue component specification, supports easycom specification)
    ├── hybrid                             存放本地网页的目录，<a href="/component/web-view">详见</a>(The directory for storing local web pages, <a href="/component/web-view">see details</a>)
    ├── pages                              业务页面文件存放的目录 (Directory where business page files are stored)
    ├── static                             存放应用引用静态资源（如图片、视频等）的目录，<b>注意：</b>静态资源只能存放于此(The directory where static resources (such as pictures, videos, etc.) referenced by the application are stored, <b>Note:</b> Static resources can only be stored here)
    ├── license.md                         插件使用协议说明(Plug-in usage agreement description)
    ├── package.json                       插件配置，必选(除此之外均`可选`)   (Plug-in configuration, required (otherwise all `optional`))                       
    ├── readme.md                          插件文档(Plug-in documentation)
    ├── changelog.md                       插件更新日志(Plugin update log)
    ├── menu.json                          如果是uniCloud admin插件，可以通过menu.json注册动态菜单，<a href="/uniCloud/admin?id=admin-%e6%8f%92%e4%bb%b6%e5%bc%80%e5%8f%91">详见 menu.json 配置</a>(If it is a uniCloud admin plugin, you can register the dynamic menu through menu.json, <a href="/uniCloud/admin?id=admin-%e6%8f%92%e4%bb%b6%e5%bc%80%e5% 8f%91">see menu.json configuration for details</a>)
	</code>
</pre>

**Tips**
- 插件目录不支持pages.json、App.vue、main.js、manifest.json、uni.scss文件，如果需要插件使用者修改这些文件内容，请在插件文档(readme.md)中详细说明。
- The plug-in directory does not support pages.json, App.vue, main.js, manifest.json, uni.scss files. If plug-in users need to modify the content of these files, please specify in the plug-in documentation (readme.md).
- 在插件内部引用资源、跳转页面时，请尽量使用相对路径。
- When referencing resources and jumping pages within the plug-in, please use relative paths as much as possible.
- 插件内components目录同样支持easycom规范，插件使用者可以直接在项目中使用插件内符合easycom规范的组件，当项目或插件内存在easycom组件冲突，编译时会给予提示，您可以通过修改组件目录及组件文件名称来解决冲突问题。
- The components directory in the plug-in also supports the easycom specification. The plug-in user can directly use the easycom-compliant components in the plug-in. When there is an easycom component conflict in the project or plug-in, a prompt will be given during compilation. You can modify the component directory and Component file name to resolve conflicts.
### 配置
#### package.json

package.json在每个`uni_modules`插件中都必须存在，包含了插件的基本信息。以下是package.json的详细配置说明
package.json must exist in every `uni_modules` plugin and contains the basic information of the plugin. The following is a detailed configuration description of package.json

```json
{
    // 注意，不能直接拷贝本段代码到编辑器中，package.json 目前不支持注释。本段代码加的注释只是用于解释代码。
   // Note that you cannot directly copy this code into the editor. Package.json currently does not support comments. The comments in this code are only used to explain the code.
	"id": "作者ID-插件英文名称(Author ID-English name of the plugin)", 
	// 必填，插件ID，格式为：'作者ID-插件英文名称'，例如：'xx-yy'，其中作者ID和插件名称只能包含英文、数字，作者ID不能使用'DCloud'、'uni'等关键字
   // Required, plug-in ID, the format is:'author ID-plug-in English name', for example:'xx-yy', where the author ID and plug-in name can only contain English and numbers, and the author ID cannot use'DCloud',' keywords such as uni'
    
	"displayName": "插件显示名称(Plug-in display name)", 
	// 必填，用于展示在插件市场的显示名称
   // Required, used to display the display name in the plug-in market
	"version": "1.0.0", 
	// 必填，插件版本
   // required, plug-in version
   
	"description": "插件描述(Plug-in description)", 
	// 必填，插件描述
   // Required, plug-in description
   
	"keywords": [], 
	// 必填，插件标签关键词，最多5个
    // Required, plug-in tag keywords, up to 5
	
	"repository": "github:user/repo", 
	// 仓库地址
	// Warehouse Address

    "engines": { 
		// HBuilderX/cli 最低兼容版本
		// HBuilderX/cli minimum compatible version

        "HBuilderX": "^3.1.0"
    },
    "dcloudext": { 
		// DCloud插件市场配置
		// DCloud plug-in market configuration

      "category": ["前端组件(Front-end components)", "通用组件(Common components)"], 
	  // 必填， 插件市场分类
	  // required, plug-in market category

      "sale": { 
		  // 销售 （目前仅限uniCloud类插件）
		  // Sale (currently only uniCloud plugins)

          "regular": { 
			  // 普通授权版价格，单位为元，如果为免费插件，设置普通授权版价格为 0 即可。
			  // The price of the normal authorized version is in yuan. If it is a free plug-in, set the price of the normal authorized version to 0.
			  
              "price": "0.00"
          },
          "sourcecode": { 
			  // 源码授权版价格，单位为元
			  // The price of the source code license version, in yuan
              "price": "0.00"
          }
      },
      "contact": { 
		  // 插件作者 QQ，方便管理员审核时与作者快速沟通。
		  // Plug-in author QQ, which is convenient for administrators to quickly communicate with the author during review.

          "qq": ""
      },
      "declaration": { 
		  // 隐私、权限及商业化声明
		  // Privacy, permissions and commercialization statement

          "ads": "", 
		  //  必填，本插件是否包含广告，如包含需详细说明广告表达方式、展示频率，请如实填写，如不包含，可填“无”
         // Required, whether this plug-in contains advertisements, if it does, it needs to specify the advertising expression and display frequency, please fill in truthfully, if not, fill in "none"

		  "data": "", 
		  // 必填，本插件采集的数据、发送的服务器地址、以及数据用途说明，请如实填写，如不采集任何数据，可填写“插件不采集任何数据”，如果使用的三方SDK需要采集数据，可填写“插件使用的 XX SDK会采集数据，详情可参考：https://other-sdk.com/"
         // Required. Please fill in the data collected by this plug-in, the server address sent, and the description of the data usage truthfully. If you do not collect any data, you can fill in "The plug-in does not collect any data". If the third-party SDK used needs to collect data, You can fill in "The XX SDK used by the plug-in will collect data. For details, please refer to: https://other-sdk.com/"

		  "permissions": "" 
		  // 必填，本插件需要申请的系统权限列表，请如实填写，如不需要任何权限，可填“无”
		  // Required, this plugin needs to apply for a list of system permissions, please fill in truthfully, if you don’t need any permissions, you can fill in "none"

      },
      "npmurl":"" 
	  // npm 地址
	  // npm address

    },
    "uni_modules": { 
		// uni_modules配置
		// uni_modules configuration

        "dependencies": [], 
		// 依赖的 uni_modules 插件ID列表
		// Dependent uni_modules plugin ID list

        "encrypt": [ 
			// 配置云函数，公共模块，clientDB Action加密
			// Configure cloud functions, public modules, clientDB Action encryption

            "uniCloud/cloudfunctions/uni-admin/controller/permission.js" 
			// 注意这里是真实的文件路径，uni_modules下的uniCloud不带-aliyun、-tcb后缀，但是项目根目录下的uniCloud是带有后缀的
			// Note that this is the real file path, uniCloud under uni_modules does not have -aliyun, -tcb suffixes, but uniCloud under the project root directory has suffixes
		],
        "platforms": { 
			// 平台兼容性：y 表示 Yes，支持；n 表示 No，不支持；u 表示 Unknown，不确定；默认为 u
			// Platform compatibility: y means Yes, support; n means No, not support; u means Unknown, not sure; the default is u

            "cloud": { 
				// 云端平台兼容性
				// Cloud platform compatibility

                "tcb": "y",
                "aliyun": "y"
            },
            "client": { 
				// 前端平台兼容性
				// Front-end platform compatibility
				
                "App": {
                    "app-vue": "y",
                    "app-nvue": "n"
                },
                "H5-mobile": {
                    "Safari": { 
						// 当需要指定最小版本才支持时，可以配置minVersion
						// When you need to specify the minimum version to support, you can configure minVersion
						
                        "minVersion": "14.0.2"
                    },
                    "Android Browser": "y",
                    "微信浏览器(Android)(WeChat browser (Android))": "u",
                    "QQ浏览器(Android)(QQ browser (Android))": "u"
                },
                "H5-pc": {
                    "Chrome": "y",
                    "IE": "u",
                    "Edge": "u",
                    "Firefox": "u",
                    "Safari": "u"
                }
            }
        }
    }
}
```



**Tips**
- 上述配置基于npm [package.json](https://docs.npmjs.com/cli/v6/configuring-npm/package-json)规范扩展，故标准的package.json属性也同样支持，比如可以通过files来控制要上传的插件包内容
- The above configuration is based on npm [package.json](https://docs.npmjs.com/cli/v6/configuring-npm/package-json) specification extension, so standard package.json attributes are also supported, for example, you can pass files to control the content of the plug-in package to be uploaded

#### uni_modules.config.json
`uni_modules.config.json`在项目根目录，可以配置插件更新后的触发脚本（通常用于执行自定义的自动化任务），插件uniCloud支持的服务空间。以下是`uni_modules.config.json`的详细配置说明
`uni_modules.config.json` In the project root directory, you can configure the trigger script (usually used to perform custom automation tasks) after the plug-in is updated, and the service space supported by the plug-in uniCloud. The following is a detailed configuration description of `uni_modules.config.json`

```json
{
	"scripts": {
		"postupdate": "node scripts/upgrade.js", 
		// 更新插件后执行该脚本，可从process.env.UNI_MODULES_ID获取当前被更新的插件ID，如果存在多个，以,隔开
		// Execute the script after updating the plug-in, you can get the currently updated plug-in ID from process.env.UNI_MODULES_ID. If there are multiple, separate them with
		"preupload": "node scripts/preupload.js", 
		// 上传插件之前执行该脚本，可从process.env.UNI_MODULES_ID获取当前被更新的插件ID，如果存在多个，以,隔开
		// Execute the script before uploading the plug-in, you can get the currently updated plug-in ID from process.env.UNI_MODULES_ID, if there are more than one, separated by
		"postupload": "node scripts/postupload.js" 
		// 上传插件之后(无论上传成功还是失败)执行该脚本，可从process.env.UNI_MODULES_ID获取当前被更新的插件ID，如果存在多个，以,隔开
		// After uploading the plug-in (regardless of whether the upload is successful or failed), execute the script, and obtain the currently updated plug-in ID from process.env.UNI_MODULES_ID. If there are multiple, separate them with
	},
	"uni_modules": {
		"uni-id": { 
			// 插件ID
			// Plugin ID
			"uniCloud": ["aliyun", "tcb"] 
			// 当项目同时存在aliyun，tcb时可手动指定该插件所属的服务空间
			// When both aliyun and tcb exist in the project, you can manually specify the service space to which the plug-in belongs
		}
	}
}
```


**Tips**
- 当项目内仅关联了一个服务空间，此时uni_modules插件内的uniCloud相关资源会自动归属至该服务空间，无需在uni_modules.config.json中配置uniCloud所属服务空间
- When only one service space is associated in the project, the uniCloud related resources in the uni_modules plugin will automatically belong to that service space, and there is no need to configure the service space of uniCloud in uni_modules.config.json
- 当项目内关联了两个服务空间（阿里云和腾讯云同时存在）
- When two service spaces are associated in the project (Alibaba Cloud and Tencent Cloud exist at the same time)
  * 若未在uni_modules.config.json中配置平台，则上传该插件uniCloud资源时，会提示上传至选择哪个服务空间
  * If the platform is not configured in uni_modules.config.json, when uploading the plugin uniCloud resources, you will be prompted to upload to which service space to choose
  * 若已在uni_modules.config.json中配置平台，则上传时以配置为准，自动归属至指定的服务空间
  * If the platform has been configured in uni_modules.config.json, the configuration will prevail when uploading, and it will automatically belong to the designated service space
 
#### npmignore@npmignore

uni_modules插件发布到插件市场是通常需要忽略掉一些目录或文件，比如`unpackage`、`.hbuilderx`、`node_modules`等，这时可以通过npmignore文件来实现文件的忽略。
When uni_modules plug-in is released to the plug-in market, it is usually necessary to ignore some directories or files, such as `unpackage`, `.hbuilderx`, `node_modules`, etc. At this time, the file can be ignored through the npmignore file.

文件名：**.npmignore**，注意开头有个点。典型的npmignore文件内容如下：
File name: **.npmignore**, note that there is a dot at the beginning. The content of a typical npmignore file is as follows:

```
.hbuilderx
unpackage
node_modules
package-lock.json
```

**注意**
**Notice**

- 项目根目录下的`.npmignore`对发布项目、插件模板生效。`uni_modules/插件Id/.npmignore`对发布插件生效
- The `.npmignore` in the project root directory is effective for publishing projects and plugin templates. `uni_modules/pluginId/.npmignore` is effective for publishing plugins

### 开发 uni_modules 插件
### Develop uni_modules plugin

#### 新建uni_modules目录
#### New uni_modules directory

在uni-app项目根目录下，创建uni_modules目录，在HBuilderX中可以项目右键菜单中点击`新建uni_modules目录`
In the root directory of the uni-app project, create a uni_modules directory, and in HBuilderX, you can click `New uni_modules directory` in the right-click menu of the project

![](https://bjetxgzv.cdn.bspapp.com/VKCEYUGU-dc-site/de27eb20-6217-11eb-8a36-ebb87efcf8c0.png)

**Tips:**
- 如果是vue-cli项目，uni_modules目录，位于`src`下，即`src/uni_modules`
- If it is a vue-cli project, the uni_modules directory is located under `src`, namely `src/uni_modules`

#### 新建uni_modules插件
#### New uni_modules plugin
1. 在HBuilderX中uni_modules目录右键点击`新建uni_modules插件`
1. Right-click the uni_modules directory in HBuilderX and click on `New uni_modules plugin`

![](https://bjetxgzv.cdn.bspapp.com/VKCEYUGU-dc-site/dd758b10-6217-11eb-8a36-ebb87efcf8c0.png)

2. 填写正确的插件ID，选择插件分类
2. Fill in the correct plug-in ID and select the plug-in category

![](https://bjetxgzv.cdn.bspapp.com/VKCEYUGU-dc-site/dcc6d480-6217-11eb-8a36-ebb87efcf8c0.png)

插件ID命名规范：
Plug-in ID naming convention:
- 格式为：'作者ID-插件英文名称'，示例：'xx-yy'，其中作者ID和插件英文名称只能包含英文、数字
- The format is:'Author ID-plug-in English name', example:'xx-yy', where the author ID and plug-in English name can only contain English and numbers
- 作者ID由插件作者自定义，不能使用'DCloud'、'uni'等关键字，长度要求至少2位字符
- The author ID is customized by the plug-in author, keywords such as'DCloud' and'uni' cannot be used, and the length must be at least 2 characters
- 插件名称需直观表达插件的作用，例如：tag、button等
- The name of the plug-in should express the function of the plug-in directly, such as tag, button, etc.
**Tips**
- `uni_modules`插件可以在package.json的`uni_modules->dependencies`节点配置三方依赖（依赖的插件也必须是`uni_modules`插件），如果是依赖了三方的npm插件，可以使用标准的dependencies节点配置。
- The `uni_modules` plugin can be configured with three-party dependencies in the `uni_modules->dependencies` node of package.json (the dependent plugin must also be the `uni_modules` plugin). If it is dependent on the three-party npm plugin, you can use the standard dependencies node configuration .


#### 发布到插件市场
#### Publish to the plug-in market

当您的插件开发完毕，可以直接发布到[插件市场](https://ext.dcloud.net.cn/)供其他人免费或付费使用，插件市场提供了变现、评价等机制，优秀的插件作者，可以做到月入好几万。
When your plug-in is developed, you can directly publish it to [plug-in market](https://ext.dcloud.net.cn/) for free or paid use by others. The plug-in market provides mechanisms for monetization and evaluation. Excellent plug-ins The author can make a monthly income of tens of thousands.

发布流程：
Release process:

1. 在HBuilderX中插件目录右键点击`发布到插件市场`
1. Right-click on "Publish to Plugin Market" in the plug-in directory in HBuilderX
![](https://bjetxgzv.cdn.bspapp.com/VKCEYUGU-dc-site/5a4b97a0-6219-11eb-8ff1-d5dcf8779628.png)
2. 填写插件信息
2. Fill in the plug-in information
![](https://bjetxgzv.cdn.bspapp.com/VKCEYUGU-dc-site/9cbc6970-6219-11eb-b997-9918a5dda011.png)
**Tips**
- 如果需要发布为项目模板，请在项目根目录创建package.json，然后右键菜单发布到插件市场。
- If you need to publish as a project template, please create package.json in the project root directory, and then right-click it to publish to the plug-in market.
- 发布插件时，可以选择上传当前项目作为示例工程，完整的示例工程，可以方便用户快速上手。
- When publishing the plug-in, you can choose to upload the current project as a sample project. The complete sample project can facilitate users to get started quickly.

#### 修改插件基本信息
#### Modify the basic information of the plug-in

当您的插件发布到插件市场后，如果需要调整插件市场上的一些基本信息，比如插件中文名称，描述，关键词，readme.md等，可以直接在插件目录右键`修改插件基本信息`
After your plug-in is released to the plug-in market, if you need to adjust some basic information on the plug-in market, such as the Chinese name of the plug-in, description, keywords, readme.md, etc., you can directly right-click the plug-in directory `modify basic information of the plug-in`

1. 在HBuilderX中插件目录右键点击`修改插件基本信息`
1. Right-click on "Modify Plug-in Basic Information" in the plug-in directory in HBuilderX
![](https://bjetxgzv.cdn.bspapp.com/VKCEYUGU-dc-site/451fb530-6225-11eb-918d-3d24828c498c.png)
2. 修改插件基本信息
2. Modify the basic information of the plug-in
![](https://bjetxgzv.cdn.bspapp.com/VKCEYUGU-dc-site/345b6910-6225-11eb-8ff1-d5dcf8779628.png)

#### 发布新版本
#### Release new version

当您的插件增加了新的功能或修复了Bug，需要发布新版本时，操作与第一次发布一样，可以直接在插件目录右键`发布到插件市场`
When your plug-in adds new features or fixes bugs, and you need to release a new version, the operation is the same as the first release, you can directly right-click the plug-in directory `publish to plug-in market`
**Tips**
- 在发布窗口中填写的更新日志，会自动与根目录的changelog.md保持同步
- The update log filled in the release window will automatically be synchronized with the changelog.md in the root directory

### 使用 uni_modules 插件
### Use uni_modules plugin

#### 添加uni_modules插件
#### Add uni_modules plugin

1. 在[插件市场](https://ext.dcloud.net.cn/)查找符合自己需求的uni_modules插件
1. Find the uni_modules plugin that meets your needs in [Plugin Market](https://ext.dcloud.net.cn/)
2. 在插件详情页,右侧会标明该插件是否支持uni_modules，点击`使用 HBuilderX 导入插件`
2. On the plug-in details page, the right side will indicate whether the plug-in supports uni_modules, click `Use HBuilderX to import plug-ins`
![](https://bjetxgzv.cdn.bspapp.com/VKCEYUGU-dc-site/3f6e2c00-622c-11eb-bdc1-8bd33eb6adaa.png)
3. 选择要导入的uni-app项目
3. Select the uni-app project to be imported
![](https://bjetxgzv.cdn.bspapp.com/VKCEYUGU-dc-site/eb6722a0-622c-11eb-a16f-5b3e54966275.png)

**Tips**
- uni_modules支持组件easycom，使用者可以直接使用插件内符合easycom规范的组件
- uni_modules supports the easycom component, users can directly use the easycom-compliant components in the plug-in
- 其他资源，如图片，js等，在项目中可以直接按目录结构引入即可使用，如：
- Other resources, such as pictures, js, etc., can be directly imported and used in the project according to the directory structure, such as:
```js
import {test} from '@/uni_modules/xx-yy/js_sdk/test.js'
```
- 如果要使用uni_modules中的页面，您需要在自己项目根目录的pages.json中添加对应的页面配置
- If you want to use pages in uni_modules, you need to add the corresponding page configuration to pages.json in the root directory of your project
```json
{
  "pages":[{
    "path":"uni_modules/xx-yy/pages/demo/demo" 
	// 按插件所在目录引入对应的页面
	// Import the corresponding page according to the directory where the plug-in is located
  }]
}
```

#### 安装uni_modules插件依赖
#### Install uni_modules plugin dependencies

1. 导入插件时，HBuilderX会自动安装当前插件的所有三方依赖。
1. When importing the plug-in, HBuilderX will automatically install all the third-party dependencies of the current plug-in.
2. 您还可以在插件目录右键手动执行`安装插件三方依赖`
2. You can also right-click the plug-in directory to manually execute `Install plug-in third-party dependencies`
![](https://bjetxgzv.cdn.bspapp.com/VKCEYUGU-dc-site/eef13280-62d6-11eb-918d-3d24828c498c.png)
#### 更新uni_modules插件
#### Update uni_modules plugin
1. 可以通过插件目录右键`从插件市场更新`，来检查更新当前所使用的插件
1. You can check and update the currently used plug-ins by right-clicking on the plug-in directory `Update from the plug-in market`
![](https://bjetxgzv.cdn.bspapp.com/VKCEYUGU-dc-site/ccb42320-622d-11eb-8ff1-d5dcf8779628.png)
2. 对比插件，确认更新内容
2. Compare the plug-in and confirm the updated content
![](https://bjetxgzv.cdn.bspapp.com/VKCEYUGU-dc-site/9069d370-62d6-11eb-a16f-5b3e54966275.png)
#### 卸载uni_modules插件
#### Uninstall uni_modules plugin
uni_modules插件目录是独立存在的，如果您不再需要该插件，可以直接删除该插件目录。
The uni_modules plugin directory exists independently. If you no longer need the plugin, you can delete the plugin directory directly.
**Tips**
- 导入uni_modules规范插件需要使用 3.1.0 以上版本的 HBuilderX
- Importing uni_modules specification plug-in requires HBuilderX version 3.1.0 or higher


### 已有插件迁移为 uni_modules 插件指南
### Migration of existing plugins to uni_modules plugin guide
1. 将插件内容迁移至您的uni-app示例项目根目录`uni_modules`下以插件ID命名的目录下，举例，若您已有的插件ID为`xx-yy`，则目录结构为：`uni_modules/xx-yy`
1. Migrate the plug-in content to the directory named after the plug-in ID under the root directory `uni_modules` of your uni-app sample project. For example, if your existing plug-in ID is `xx-yy`, the directory structure is:` uni_modules/xx-yy`
2. 运行自己的示例项目，验证插件迁移目录后，所有功能是否正常
2. Run your own sample project to verify whether all functions are normal after the plug-in migration directory
 - 目录迁移，通常会遇到资源引用路径问题，尽可能将所有路径引用修改为相对路径
 - Directory migration usually encounters resource reference path problems, as far as possible, modify all path references to relative paths
 - 如果插件带有uniCloud的云函数或数据库，迁移时，注意，插件目录内的uniCloud不能带有厂商后缀，您可以在发布插件时，指定插件支持的云服务商
 - If the plug-in comes with uniCloud cloud functions or databases, when migrating, please note that uniCloud in the plug-in directory cannot have a vendor suffix. You can specify the cloud service provider supported by the plug-in when publishing the plug-in
 - 插件目录不支持pages.json、App.vue、main.js、manifest.json、uni.scss文件，如果需要插件使用者修改这些文件内容，请在插件文档(readme.md)中详细说明。
 - The plug-in directory does not support pages.json, App.vue, main.js, manifest.json, uni.scss files. If plug-in users need to modify the content of these files, please specify in the plug-in documentation (readme.md).
3. 当迁移后的所有插件功能均正常时，您就可以向插件市场发布新的支持uni_modules的插件版本（插件市场会同时保留您最后一个非uni_modules插件版本）
3. When all the plug-in functions after migration are normal, you can release a new plug-in version that supports uni_modules to the plug-in market (the plug-in market will also retain your last non-uni_modules plug-in version)
 - 在插件根目录创建package.json，您可以先简单的仅填写一个插件ID即可，其他信息可以通过发布窗口填写（会自动同步回package.json）
 - Create package.json in the plug-in root directory, you can simply fill in a plug-in ID first, and other information can be filled in through the release window (it will be automatically synchronized back to package.json)

```
{
  "id":"您的插件ID(Your plugin ID)"
}
```
 - 插件文档，迁移至插件根目录的readme.md中
 - Plug-in documentation, migrated to readme.md in the root directory of the plug-in
 - 右键package.json，点击`发布到插件市场`，选择分类，填写插件信息（尽可能与插件市场已有信息保持一致）
 - Right-click package.json, click `Publish to plug-in market`, select the category, and fill in the plug-in information (as much as possible to be consistent with the existing information in the plug-in market)
 - 发布成功后，您可以在插件市场的插件详情页右侧，查看到您的插件已同时提供了uni_modules版本和非uni_modules版本（仅保留最后一个非uni_modules版本）
 - After the release is successful, you can check on the right side of the plug-in details page of the plug-in market that your plug-in has provided both the uni_modules version and the non-uni_modules version (only the last non-uni_modules version is retained)
![](https://bjetxgzv.cdn.bspapp.com/VKCEYUGU-dc-site/47c2a2f0-62db-11eb-a16f-5b3e54966275.png)
