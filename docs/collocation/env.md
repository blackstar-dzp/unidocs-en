uni-app 项目中配置环境变量主要有如下三种方式：
There are three main ways to configure environment variables in uni-app projects:

### vue-config.js

在 vue.config.js 中可以修改 webpack 配置，包括环境变量，具体参考 [vue-config.js](/collocation/vue-config)。
You can modify webpack configuration in vue.config.js, including environment variables. For details, please refer to [vue-config.js](/collocation/vue-config).

### package.json

在自定义条件编译平台时，可以在 package.json 文件的 env 节点下配置环境变量，具体参考 [package.json](/collocation/package)
When customizing the conditional compilation platform, you can configure environment variables under the env node of the package.json file. For details, refer to [package.json](/collocation/package)

### .env

CLI 创建的项目中可以在根目录中放置 ``.env`` 文件来指定环境变量，具体参考：[环境变量](https://cli.vuejs.org/zh/guide/mode-and-env.html#%E7%8E%AF%E5%A2%83%E5%8F%98%E9%87%8F)。
In the project created by CLI, you can place a ``.env'' file in the root directory to specify environment variables. For details, please refer to: [Environmental Variables](https://cli.vuejs.org/zh/guide/mode-and-env .html#%E7%8E%AF%E5%A2%83%E5%8F%98%E9%87%8F).