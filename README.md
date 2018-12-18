## weex 中集成 F2 实现图表功能
> 环境
- macOS: `v10.14.1`
- nodeJS: `v8.12.0`
- npm: `v6.4.1`
- weex: `v1.3.11`
- WeexSDK: `0.20.1`
- WeexGcanvas: `0.1.2`
- F2: `3.1.0`

> 运行工程

```
// 进入工程
cd weeTest

// 安装 npm 包
npm install

// 安装 ios 插件
cd platforms/ios
pod install

// 运行模拟器
weex run ios
```

> 坑点
- App store 目前下载的 weex playground 不集成 Gcanvas。所以直接下载的无法展示
