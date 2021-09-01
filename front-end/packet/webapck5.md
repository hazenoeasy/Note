https://webpack.docschina.org/concepts/#entry
# webpack 是啥
es6 less 等浏览器不能识别的代码 需要对代码进行预编译 ->构建工具   

index.js 入口文件  会引入各种资源，形成chunk(代码块)

chunk 进行打包编译  输出 bundle

所以webpack是静态资源 打包器

# webpack 核心概念
* entry  入口起点
* output bundles输出以及命名
* loader 帮助处理非js文件(css,img...)
* plugins 可以做更多功能，如打包优化，压缩
* mode 开发模式 生产化境

# 引入图片
css 图片  url-loader 默认使用es6模块化解析
html 图片   html-loader 负责引入img 从而能被url-loader处理 使用commonjs  可以手动关闭url-loaderes6
# configureWebpack devtool:'sourcemap'