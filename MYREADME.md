# 一、初始模版选择建议
1、 如果是线上项目，建议将 components 的内容也进行清理，以免影响访问速度，或者直接使用 vue-admin-template 构建项目。
2、课程选择 vue-element-admin 初始化项目，是因为 vue-element-admin 实现了登录模块，包括 token 校验、网络请求等，可以简化我们的开发工作。
npm run dev
http://www.youbaobao.xyz/admin-docs/guide/exercise/login.html


# 二、src 的settings.js 的配置原理
title: '小慕读书'
1、title原理：
(1)、ctrl + shift + F ->settings.title
get-page-title.js
(2)、ctrl + shift + F ->get-page-title


2、showSettings:true  # 旁边的控制面板

3、tagsView:true  # 置顶 导航

4、fixedHeader:false # 头部跟随

5、sidebarLogo:false # logo展示


6、errorLog：'production' # 是否记录错误日志


# 三、如何调试
vue.config.js  有一个config.devtool 
原来值：cheap-source-map
改为：source-map   适合调试
改好后，浏览器下面的source会变成源码

推荐改为：eval  缺点，不能还原源码   适合开发，加快构建速度



# 四、项目结构  需要多听几次！！！
api：接口请求
assets：静态资源
components：通用组件
directive：自定义指令
filters：自定义过滤器
icons：图标组件
layout：布局组件
router：路由配置
store：状态管理
styles：自定义样式
utils：通用工具方法
auth.js：token 存取
permission.js：权限检查
request.js：axios 请求封装
index.js：工具方法
views：页面
permission.js：登录认证和路由跳转
settings.js：全局配置
main.js：全局入口文件
App.vue：全局入口组件


# 五、bug
## 1、开发过程中可能会碰到 script 标签中源码的 eslint 关于 indent 的报错
script 格式化问题
通过 command + option + L 格式化代码后，script 可能会出现 indent 的警告，解决方案有两种：
关闭 eslint 中的 indent 检查；
修改 webstorm 中 indent 设置：
Webstorm => Preferences => Editor => Code Style => HTML => Other
在 do not indent of children 中增加 script 即可


# 六、代码整理
1、code -> format Code

2、script 格式化问题
通过 command + option + L 格式化代码后，script 可能会出现 indent 的警告，解决方案有两种：
关闭 eslint 中的 indent 检查；
修改 webstorm 中 indent 设置：
Webstorm => Preferences => Editor => Code Style => HTML => Other
在 do not indent of children 中增加 script 即可