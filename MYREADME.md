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



# 路由
## 路由和权限验证
### 源码解析
```javascript
<script>
    router.beforeEach(async(to, from, next) => {
    // 启动进度条
    NProgress.start()
  
    // 修改页面标题
    document.title = getPageTitle(to.meta.title)
  
    // 从 Cookie 获取 Token
    const hasToken = getToken()
  
    // 判断 Token 是否存在
    if (hasToken) {
    // 如果当前路径为 login 则直接重定向至首页
    if (to.path === '/login') {
    next({ path: '/' })
    NProgress.done()
  } else {
    // 判断用户的角色是否存在
    const hasRoles = store.getters.roles && store.getters.roles.length > 0
    // 如果用户角色存在，则直接访问
    if (hasRoles) {
    next()
  } else {
    try {
    // 异步获取用户的角色
    const { roles } = await store.dispatch('user/getInfo')
    // 根据用户角色，动态生成路由
    const accessRoutes = await store.dispatch('permission/generateRoutes', roles)
    // 调用 router.addRoutes 动态添加路由
    router.addRoutes(accessRoutes)
    // 使用 replace 访问路由，不会在 history 中留下记录
    next({ ...to, replace: true })
  } catch (error) {
    // 移除 Token 数据
    await store.dispatch('user/resetToken')
    // 显示错误提示
    Message.error(error || 'Has Error')
    // 重定向至登录页面
    next(`/login?redirect=${to.path}`)
    NProgress.done()
  }
  }
  }
  } else {
    // 如果访问的 URL 在白名单中，则直接访问
    if (whiteList.indexOf(to.path) !== -1) {
    next()
  } else {
    // 如果访问的 URL 不在白名单中，则直接重定向到登录页面，并将访问的 URL 添加到 redirect 参数中
    next(`/login?redirect=${to.path}`)
    NProgress.done()
  }
  }
  })
  
    router.afterEach(() => {
    // 停止进度条
    NProgress.done()
  })
  
</script>
```




# 界面
## 侧边栏

## 面包屑导航


