vue.config.js 是一个可选的配置文件，如果项目的根目录中存在这个文件，那么它会被自动加载，一般用于配置 webpack 等编译选项，具体规范参考：[vue.config.js](https://cli.vuejs.org/zh/config/#vue-config-js)
vue.config.js is an optional configuration file. If this file exists in the root directory of the project, it will be automatically loaded. It is generally used to configure compilation options such as webpack. For specific specifications, refer to: [vue.config.js](https://cli.vuejs.org/config/#global-cli-config)

**支持情况**
**Support situation**
* CLI 工程 
* CLI project
* HBuilderX 2.1.5 及以上版本
* HBuilderX 2.1.5 and above

**注意事项**
**Precautions**

- 仅vue页面生效
- Only the vue page takes effect

部分配置项会被编译配置覆盖，例如：
Some configuration items will be overwritten by the compiled configuration, for example:

* publicPath  不支持，如果需要配置，请在 manifest.json->h5->router->base 中配置，参考文档：[h5-router](collocation/manifest?id=h5-router)
* PublicPath does not support. If you need to configure it, please configure it in manifest.json->h5->router->base
* outputDir  不支持
* outputDir does not support
* assetsDir 固定 static
* assetsDir fixed static
* pages  不支持
* pages not supported
* runtimeCompiler 固定 false
* runtimeCompiler fixed false
* productionSourceMap 固定 false
* productionSourceMap fixed false
* css.extract  H5 平台固定 false，其他平台固定 true
* css.extract H5 platform fixed false, other platforms fixed true
* parallel 固定 false
* parallel fixed false
* 使用cli项目时，默认情况下 babel-loader 会忽略所有 node_modules 中的文件。如果你想要通过 Babel 显式转译一个依赖，可以在transpileDependencies中列出来。[详情参考](https://cli.vuejs.org/zh/config/#transpiledependencies)
* When using the cli project, babel-loader will ignore all files in node_modules by default. If you want to explicitly translate a dependency through Babel, you can list it in transpileDependencies. [For details](https://cli.vuejs.org/config/#transpiledependencies)

**使用示例**
**Usage example**

**自定义静态资源目录**
**Custom static resource directory**

```js
const path = require('path')
//最新版本copy-webpack-plugin插件暂不兼容，推荐v5.0.0
//The latest version of the copy-webpack-plugin is currently not compatible. V5.0.0 is recommended
const CopyWebpackPlugin = require('copy-webpack-plugin')

module.exports = {
	configureWebpack: {
		plugins: [
			new CopyWebpackPlugin([
				{
					from: path.join(__dirname, 'src/images'),
					to: path.join(__dirname, 'dist', process.env.NODE_ENV === 'production' ? 'build' : 'dev', process.env.UNI_PLATFORM, 'images')
				}
			])
		]
	}
}
```

**注入全局依赖**
**Inject global dependencies**

```js
const webpack = require('webpack')

module.exports = {
	configureWebpack: {
		plugins: [
			new webpack.ProvidePlugin({
				'localStorage': ['mp-storage', 'localStorage'],
				'window.localStorage': ['mp-storage', 'localStorage']
			})
		]
	}
}
```

**配置环境变量**
**ENV**

```js
const webpack = require('webpack')

module.exports = {
  chainWebpack: config => {
    config
      .plugin('define')
      .tap(args => {
        args[0]['process.env'].VUE_APP_TEST = '"test"'
        return args
      })
  }
}
```

**发布时删除console**
**Delete console when publishing**

`HBuilderX 2.6.8+`支持
`HBuilderX 2.6.8+`stand by

```js
module.exports = {
	chainWebpack: (config) => {
		// 发行或运行时启用了压缩时会生效
    // This takes effect when compression is enabled at release or runtime
		config.optimization.minimizer('terser').tap((args) => {
			const compress = args[0].terserOptions.compress
			// 非 App 平台移除 console 代码(包含所有 console 方法，如 log,debug,info...)
      // Non-App platforms remove Console code (including all Console methods, such as log,debug,info...)
			compress.drop_console = true
			compress.pure_funcs = [
				// App 平台 vue 移除日志代码
				// App platform VUE removes logging code
				'__f__', 
				// 可移除指定的 console 方法
				//Removes the specified Console method
				// 'console.debug'
			]
			return args
		})
	}
}
```
