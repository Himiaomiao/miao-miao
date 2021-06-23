# webpack学习

## 1、webpack的安装

>注意：需要先自行安装node.js环境
>
>+ 全局安装
>
>  ```javascript
>  npm i webpack webpack-cli -g
>  ```
>
>+ 项目中安装webpack
>
>  ```javascript
>  npm i webpack webpack-cli -D
>  ```

## 2、webpack的使用

>### 2.1. wepback-cli
>
>npm 5.2 以上的版本中提供npx命令
>
>npx想要解决的主要问题，就是调用项目内部安装的模块，原理就是在node_modules下的.bin目录中找到对应的命令执行
>
>使用wepback命令：`npx webpack`
>
>webpack4之后可以实现0配置打包构建，0配置的特点就是限制较多，无法自定义很多配置，开发中常用的还是使用webpack配置进行打包构建
>
>### 2.2. webpack配置
>
>webpack有四大核心概念
>
>+ 入口（entry）：程序的入口js
>
>+ 输出（output）：打包后存放的位置
>
>+ loader:用于对模块的源码进行转换
>
>+ 插件(plugins)：插件目的在于解决loader无法实现的其他事
>
>`官方文档定义webpack配置文件的名字为webpack.config.js`
>
>1、配置webpack.config.js
>
>2、运行webpack
>
>配置示例：
>
>```javascript
>const path = require('path');
>
>module.exports = {
>   //入口文件配置
> entry: './path/to/my/entry/file.js',
>   //出口文件配置
> output: {
>     //输出的路径,webpack2起就规定必须是绝对路径
>   path: path.resolve(__dirname, 'dist'),
>     //输出文件名字
>   filename: 'my-first-webpack.bundle.js',
> },
>   //mode默认为production，可以手动设置为development，区别就是打包的时候是否进行代码压缩混合
>   mode:'development'
>};
>
>```
>
>
>
>### 2.3.项目自定义执行命令
>
>npm提供在`package.json`文件下的`scripts`命令下可以自己定义命令
>
>### 2.4. 开发时自动编译工具
>
>每次要编译代码时，手动运行npm run build就会变得很麻烦
>
>webpack中有几个不同的选项，可以帮助你在代码发生变化后自动编译代码
>
>1. webpack's Watch Mode
>2. webpack-dev-server
>3. webpack-dev-middleware
>
>多数场景中，可能需要使用`webpack-dev-server`
>
>#### 2.3.1. watch
>
>在`webpack`指令后面加上`--watch`参数即可
>
>主要的作用就是监视本地项目文件的变化，发现有修改的代码会自动编译打包，生成输出文件
>
>1、配置`package.json`的scripts`"watch":webpack --watch`
>
>2、运行`npm run watch`
>
>以上是cli的方式设置watch的参数
>
>还可以通过配置文件对watch的参数进行修改：
>
>```javascript
>const path = require('path');
>
>module.exports = {
>  //入口文件配置
>  entry: './src/index.js',
>  //出口文件配置
>  output: {
>      //输出的路径,webpack2起就规定必须是绝对路径
>      //path.resolve解析当前的相对路径为绝对路径
>      path: path.resolve('./dist/'),
>      //输出文件名字
>      filename: 'my-first-webpack.bundle.js',
>  },
>  mode: 'production',
>  //开启监视模式，此时执行webpack指令进行打包会监视文件变化自动打包
>  watch:true
>};
>```
>
>
>
>#### 2.3.2.webpack-dev-server(官网推荐使用)
>
>1、安装`devServer`:
>
>`devServer`需要依赖`webpack`,必须在项目依赖中安装`webpack`
>
>`npm i webpack-dev-server webpack -D`
>
>2、index.html中修改`<script src="/bundle.js"></script>`
>
>3、运行：`npx webpack server`
>
>4、运行：`npx webpack server --hot --open --port 8090`
>
>5、配置`package.json`的scripts:`"dev":"webpack server --hot --open --port 8090"`
>
>6、运行`npm run dev`
>
>devServer会在内存中生成一个打包好的`bundle.js`，专供开发时使用，打包效率高，修改代码后会自动重新打包以及刷新浏览器，用户体验非常好
>
>以上是cli的方式设置对devServer的参数
>
>还可以通过配置文件对devServer的参数进行修改：
>
>```javascript
>const path = require('path');
>
>module.exports = {
>  //入口文件配置
>  entry: './src/index.js',
>  //出口文件配置
>  output: {
>      //输出的路径,webpack2起就规定必须是绝对路径
>      //path.resolve解析当前的相对路径为绝对路径
>      path: path.resolve('./dist/'),
>      //输出文件名字
>      filename: 'bundle.js',
>  },
>  mode: 'production',
>  //开启监视模式，此时执行webpack指令进行打包会监视文件变化自动打包
>  //watch: true
>  //配置devServer参数
>  devServer: {
>      //是否自动打开
>      open: true,
>      //定义开启的端口号
>      port: 3000,
>      //压缩是否启用
>      compress: true,
>      //指定项目根目录,此时可以把项目的.html文件放在目录下，会自动打开此文件
>      contentBase: './src',
>      //开启热更替
>      hot: true
>  }
>};
>```
>
>配置`package.json`的scripts:`"dev":"webpack server"`
>
>运行`npm run dev`
>
>#### 2.3.3. html插件
>
>1、安装html-webpack-plugin插件`npm i html-webpack-plugin -D`
>
>2、在`webpack.config.js`中的`plugins`节点下配置
>
>```javascript
>const HtmlWebpackPlugin = require('html-webpack-plugin')
>plugins:[
>  new HtmlWebpackPlugin({
>      filename:'index.html',
>      template:'template.html'
>  })
>]
>```
>
>1、devServer时根据模板在express项目根目录下生成html文件(类似于devServer生成内存中的bundle.js)
>
>2、devServer时自动引入bundle.js
>
>3、打包时会自动生成index.html
>
>### 2.3.4.webpack-dev-middleware
>
>`webpack-dev-middleware`是一个容器(wrapper)，它可以把webpack处理后的文件传递给一个服务器(server)。`webpack-dev-server`在内部使用它，同时，它也可以作为一个单独的包来使用，以便进行更多自定义设置来实现更多的需求。
>
>1、安装`express`和`webpack-dev-middleware`:
>
>`npm i express webpack-dev-middleware -D`
>
>2、新建`server.js`
>
>```javascript
>const express = require('express');
>const webpack = require('webpack');
>const webpackDevMiddleware = require('webpack-dev-middleware');
>//引入配置文件
>const config = require('./webpack.config.js')
>const app = express();
>const compiler = webpack(config);
>app.use(webpackDevMiddleware(compiler,{
>  publicPath:'/'
>}));
>app.listen(3000,function(){
>  console.log('http://localhost:3000')
>})
>```
>
>3、配置`package.json`中的scripts:`"server":"node server.js"`
>
>4、运行：`npm run server`
>
>注意：如果要使用middleware,必须使用`html-webpack-plugin`插件，否则文件无法正确输出到express服务器的根目录
>
>#### 2.3.5.小结
>
>只有在开发时才需要使用自动编译工具，例如：webpack-dev-server
>
>项目上线时都会直接使用webpack进行打包构建，不需要使用这些自动编译工具
>
>自动编译工具只是为了“提高开发体验”
>
>### 2.4.处理css
>
>1. 安装`npm i css-loader style-loader -D`
>
>2. 配置`webpack.config.js`
>
> ```javascript
> module:{
>     rules:[
>          //配置的是用来解析.css文件的loader(style-loader和css-loader)
>         {
>        //用正则匹配当前访问的文件的后缀名是.css
>             test:/\.css$/,
>             //webpack底层调用这些包的顺序是从右到左
>             //css-loader:解析css文件
>             //style-loader:将解析出来的结果放到html中，使其生效
>             use:['style-loader','css-loader']
>         }
>     ]
> }
> ```
>
>
>
>### 2.5.处理less和sass
>
>使用方法和处理css文件一致
>
>`npm i less less-loader node-sass sass-loader -D`
>
>```javascript
>//写less需要基于css的两个loader
>{test:/\.less$/,use:['style-loader','css-loader','less-loader']}
>```
>
>```javascript
>//sass文件的后缀可能为sass或者scss
>{test:/\.s(a|c)ss$/,use:['style-loader','css-loader','sass-loader']}
>```
>
>
>
>### 2.6.处理图片和字体
>
>1、`npm i file-loader url-loader -D`
>
>url-loader封装了file-loader
>
>```javascript
>{
>  test:/\.(png|jpg|gif)/,
>      use:[{
>          loader:'url-loader',
>          options:{
>              //limit表示如果图片大于5kB,就以路径形式展示，小于的话就用base64格式展示
>              limit:5 * 1024,
>              //定义图片打包后输出的路径
>              outputPath:'images'
>          }
>      }]
>}
>```
>
>### 2.7.babel-loader
>
>1. `npm i babel-loader @babel/core @babel/preset-env webpack -D`
>
>2. 如果需要支持更高级的ES6语法，可以继续安装插件：
>
> `npm i @babel/plugin-properties -D`
>
> 也可以根据需要在babel官网找插件进行安装
>
> ```javascript
> {
>     test:/\.js$/,
>         use:{
>             loader:'babel-loader',
>                 options:{
>                     //配置语法预设
>                     presets:['@babel/env'],
>                         //配置插件，插件类型可以在babel官网找到
>                         plugins:['@babel/plugin-proposal-class-properties']
>                 }
>         }
>     //不需要打包的文件
>     exclude:/node_modules/
> }
> ```
>
> 官方更建议的做法是在项目根目录下新建一个.babelrc的babel配置文件
>
> ```javascript
> {
>     "presets":["@babel/env"],
>         "plugins":["@babel/plugin-proposal-class-properties"]
> }
> ```
>
> 3. 如果需要使用`generator`,无法直接使用babel进行转换，因为会将`generator`转换为一个`regeneratorRuntime`,然后使用`mark`和`wrap`来实现`generator`,但由于babel并没有内置`regeneratorRuntime`,所以无法直接使用，需要安装插件：
>
>    `npm i @babel/plugin-transform-runtime -D`
>
>    同时还需要安装运行时依赖：
>
>    `npm i @babel/runtime -S`
>
>    在`.babelrc`中添加插件：
>
>    ```javascript
>    {
>        "presets":[
>            "@babel/env"
>        ],
>            "plugins":[
>                "@babel/plugin-proposal-class-properties",
>                "@babel/plugin-transform-runtime"
>            ]
>    }
>    ```
>
>    4. 如果需要使用ES6/7中对象原型提供的新方法，babel默认情况无法转换，即使用了`trandform-runtime`的插件也不支持转换原型上的方法
>
>       需要使用另外一个模块：
>
>       `npm i @babel/polyfill -s`
>
>       该模块需要在使用新方法的地方直接引入：
>
>       `import '@babel/polyfill'`
>
>    ### 2.8.source map 的使用
>
>    #### 2.8.1. devtool
>
>    此选项控制是否生成，以及如何生成source map。
>
>    使用`SourceMapDevToolPlugin`进行更细粒度的配置，查看`source-map-loader`来处理已有的source map。选择一种source map格式来增强调式过程。不同的值会明显影响到构建(build)和重新构建(rebuild)的速度。
>
>    >可以直接使用`SourceMapDevToolPlugin/EvalSourceMapDevToolPlugin`来替代使用`devtool`选项，它有更多的选项，但是切忽同时使用`devtool`选项和`SourceMapDevToolPlugin/EvalSourcMapDevToolPlugin`插件。因为`devtool`选项在内部添加过这些插件，所以会应用两次插件。
>
>| devtool                        | 构建速度 | 重新构建速度 | 生产环境 | 品质                 |
>| ------------------------------ | -------- | ------------ | -------- | -------------------- |
>| (none)                         | +++      | +++          | yes      | 打包后的代码         |
>| eval                           | +++      | +++          | no       | 生成后的代码         |
>| cheap-eval-source-map          | +        | ++           | no       | 转换过的代码(仅限行) |
>| cheap-module-eval-source-map   | 0        | ++           | no       | 原始源代码(仅限行)   |
>| eval-source-map                | --       | +            | no       | 原始源代码           |
>| cheap-source-map               | +        | 0            | no       | 转换过的代码(仅限行) |
>| cheap-module-source-map        | 0        | -            | no       | 原始源代码(仅限行)   |
>| inline-cheap-source-map        | +        | 0            | no       | 转换过的代码(仅限行) |
>| inline-cheap-module-source-map | 0        | -            | no       | 原始源代码(仅限行)   |
>| source-map                     | --       | --           | yes      | 原始源代码           |
>| inline-source-map              | --       | --           | no       | 原始源代码           |
>| hidden-source-map              | --       | --           | yes      | 原始源代码           |
>| nosources-source-map           | --       | --           | yes      | 无源代码内容         |
>
>#### 2.8.2.这么多模式哪个好？
>
>开发环境推荐：
>
>cheap-module-eval-source-map
>
>生产环境推荐：
>
>none(不使用source map)
>
>原因如下：
>
>1. **使用cheap模式可以大幅度提高source map生成效率**。大部分情况我们调式并不关心列信息，而且就算source map没有列，有些浏览器引擎(例如v8)也会给出列信息。
>
>2. **使用module可支持babel这种预编译工具，映射转换前的代码**。
>
>3. **使用eval方式可大幅度提高持续构建效率。**官方文档提供的速度对比表格可以看到eval模式的重新构建速度都很快。
>
>4. **使用eval-source-map模式可以减少网络请求。**这种模式开启DataUrl本身包含完整sourcemap信息，并不需要像sourceURL那样，浏览器需要发送一个完整请求去获取sourcemap文件，这会略微提高点效率。而生产环境中则不宜用eval,这样会让文件变得极大。
>
>  ### 2.9.插件
>
>  #### 2.9.1.clean-webpack-plugin
>
>  该插件可以用于自动清除`dist`目录后重新生成，在`npm run build`时非常方便
>
>  1.安装插件
>
>  `npm i clean-webpack-plugin -D`
>
>  2.在webpack.config.js引入插件
>
>  ```javascript
>  const CleanWebpackPlugin = require('clean-webpack-plugin')
>  ```
>
>  3.使用插件，在plugins中直接创建对象即可
>
>  ```javascript
>  plugins:[
>      new HtmlWebpackPlugin({
>          filename:'index.html',
>          template:'./src/index.html'
>      }),
>      new CleanWebpackPlugin()
>  ]
>  ```
>
>  #### 2.9.2. copy-webpack-plugin
>
>  1.安装插件
>
>  `npm i copy-webpack-plugin -D`
>
>  2.引入插件
>
>  ```javascript
>  const CopywebpackPlugin = require('copy-webpack-plugin')
>  ```
>
>  3.使用插件，在plugin中插件对象并配置源和目标
>
>  from:源，从哪里拷贝，可以是相对路径或绝对路径，推荐绝对路径
>
>  to:目标，拷贝到哪里去，相对于`output`的路径，同样可以相对路径或绝对路径，但更推荐相对路径(直接算相对dist目录即可)
>
>  ```javascript
>  plugins:[
>      new HtmlwebpackPlugin({
>          filename:'index.html',
>          template:'./src/index.html'
>      }),
>      new CleanwebpackPlugin(),
>       new CopywebpackPlugin({
>              patterns: [
>                  {
>                      from: path.join(__dirname, 'assets'),
>                      to: 'assets'
>                  }
>              ]
>          })
>  ]
>  ```
>
>#### 2.10.BannerPlugin
>
>这是一个webpack的内置插件，用于给打包的JS文件加上版权注释信息
>
>1.引入webpack插件
>
>```javascript
>const webpack = require('webpack')
>```
>
>2.创建插件对象
>
>```javascript
>plugins:[
>    new HtmlwebpackPlugin({
>        filename:'index.html',
>        template:'./src/index.html'
>    }),
>    new CleanwebpackPlugin(),
>     new CopywebpackPlugin({
>            patterns: [
>                {
>                    from: path.join(__dirname, 'assets'),
>                    to: 'assets'
>                }
>            ]
>        }),
>    new webpack.BannerPlugin('黑马程序员牛逼！')
>]
>```
>
>

## 3、webpack高级配置

>### 3.1 HTML中img标签的图片资源处理
>
>1. 安装`npm install -s html-withimg-loader`
>
>2. 在`webpack.config.js`文件中添加loader
>
> ```javascript
> {
>     test:/\.(htm|html)$/i,
>         loader:'html-withimg-loader'
> }
> ```
>
> ### 3.2 多页应用打包
>
> 1. 在`webpack.config.js`中修改入口和出口配置
>
>    ```javascript
>    // 1.修改为多入口
>    entry:{
>        main:'./src/main.js',
>            other:'./src/other.js'
>    },
>        output:{
>            path:path.join(__dirname,'./dist'),
>                //filename:'bundle.js',
>                //2.多入口无法对应一个固定出口，所以修改filenamr为[name]变量
>                filename:'[name].js',
>                    publicPath:'/'
>        },
>            plugins:[
>                //3.如果用了html插件，需要手动配置多入口对应的html文件，将指定其对应的输出文件
>                new HtmlWebpackPlugin({
>                    template:'./index.html',
>                    filename:'index.html',
>                    chunks:['main']
>                }),
>                 new HtmlWebpackPlugin({
>                    template:'./index.html',
>                    filename:'other.html',
>                    chunks:['other']
>                }),
>       
>            ]
>    ```
>
>    2. 修改入口对象，支持多个js入口，同时修改output输出的文件名为`[name].js`，表示自己定义的入口文件为输出文件名，但是`html-webpack-plugin`不支持此功能，所以需要再拷贝一份插件，用于生成两个html页面，实现多页应用
>
>### 3.3.第三方库的两种引入方式
>
>可以通过`expose-loader`进行全局变量的注入，同时也可以使用内置插件`webpack.ProvidePlugin`对每个模块的闭包空间，注入一个变量，自动加载模块，而不必到处`import`或`require`
>
>+ expose-loader将库加载到全局作用
>
>1. 安装`expose-loader`
>
>   `npm i -D expose-loader`
>
>2. 配置loader
>
>   ```javascript
>   module:{
>       rules:[{
>           test:require.resolve('jquery'),
>           use:{
>               loader:'expose-loader',
>               options:'$'
>           }
>       }]
>   }
>   ```
>
>   tips:`require.resolve`用来获取模块的绝对路径，所以这里的loader只会作用于jquery模块，并且只在bundle中使用到它时，才进行处理。
>
>+ webpack:ProvidePlugin将库加载到模块
>
>1. 引入webpack
>
>   ```javascript
>   const webpack = require('webpack')
>   ```
>
>2. 创建插件对象
>
>   要自动加载`jquery`，我们可以将两个变量都指向对应的node模块
>
>   ```javascript
>   new webpack.ProvidePlugin({
>       $:'jquery',
>       jQuery:'jquery'
>   })
>   ```
>
>
>
>### 3.4.Development/Production不同配置文件打包
>
>项目开发时一般需要使用两套配置文件，用于开发阶段打包（不压缩代码，不优化代码，增加效率）和上线阶段打包(压缩代码、优化代码、打包后直接上线使用)
>
>抽取三个配置文件：
>
>+ webpack.base.js
>+ webpack.prod.js
>+ webpack.dev.js
>
>步骤如下：
>
>1. 将开发环境和生产环境公用配置放入base中，不同的配置各自放入prod或dev文件中(例如：mode)
>
>2. 然后在dev和prod中使用`webpack-merge`把自己的配置与base配置进行合并后导出
>
>   `npm install webpack-merge -D`
>
>3. 将package.json中的脚本参数进行修改，通过`--config`手动指定特定配置文件。
>
>### 3.5 打开打包后的dist目录
>
>1. 安装`live-server`插件
>
>   `npm install live-server -D`
>
>2. 在`package.json`中配置
>
>   `"start":live-server ./dist`
>
>### 3.6定义环境变量
>
>除了区分不同的配置文件进行打包，还需要在开发时知道当前的环境是开发阶段或上线阶段，所以可以借助内置插件`DefinePlugin`来定义环境变量，最终可以实现开发阶段与上线阶段的api地址自动切换。
>
>1.引入webpack
>
>```javascript
>const webpack = require('webpack')
>```
>
>2.创建插件对象，并定义环境变量
>
>```javascript
>new webpack.DefinePlugin({
>    IS_DEV:'false'//通过判断"IS_DEV的真假来控制接口地址"
>})
>```
>
>3.在src打包的代码环境下可以直接使用
>
>### 	3.6.使用devServer解决跨域问题
>
>在开发阶段很多时候需要使用到跨域，何为跨域，看下图
>
>![报修活动图.png](https://i.loli.net/2021/06/20/3Q1AoR4iU8ta9dy.png)
>
>开发阶段往往会遇到上面这种情况，也许将来上线后，前端项目会和后端项目部署在同一个服务器下，并不会有跨域问题，但是由于开发时会用到webpack-dev-server,所以一定会产生跨域的问题
>
>目前解决跨域主要的方案有：
>
>1. jsonp
>
>2. cors
>3. http proxy
>
>此处介绍使用devServer解决跨域，其实原理就是http proxy
>
>将所有ajax请求发送给devServer服务器，再由devServer服务器做一次转发，发送给数据接口服务器，由于ajax请求是发送给devServer服务器的，所以不存在跨域，而devServer用于是用node平台发送的http请求，自然不涉及到跨域问题，可以完美解决
>
>![报修活动图 _1_.png](https://i.loli.net/2021/06/20/Wryf2XTj4bFq3J7.png)
>
>服务器代码（返回一段字符串即可）
>
>```javascript
>const express = require('express')
>const app = express()
>// 使用cors解决跨域问题
>//const cors = require('cors')
>//app.use(cors())
>app.get('/api/getUserInfo',(req,res)=>{
>    res.send({
>        name:'黑马',
>        age:13
>    })
>    app.listen(9999,()=>{
>        console.log('http://localhost:9999!')
>    })
>})
>```
>
>前端需要配置devServer的proxy功能，在`webpack.dev.js`中进行配置：
>
>```javascript
>devServer:{
>    open:true,
>        hot:true,
>            compress:true,
>                post:3000,
>                    proxy:{
>                        //后端请求地址
>                        '/api':'http://localhost:9999'
>                    }
>}
>```
>
>意为前端请求`api`的url时，webpack-dev-server会将请求转发给`http://localhost:9999/api`处，此时如果请求地址为`http"//localhost:9999/api/getUserInfo`,只需要直接写`/api/getUserInfo`即可，代码如下：
>
>```javascript
>axios.get('/api/getUserInfo').then(res => console.log(res))
>```
>
>### 3.7. HMR的使用
>
>需要对某个模块进行热更新时，可以通过`module.hot..accept`方法进行文件监视，只要模块内容发生变化，就会触发回调函数，从而可以重新读取模块内容，做对应的操作
>
>```javascript
>if(module.hot){
>    module.hot.accept('./hotmodule.js',function(){
>        //当hotmodule.js模块内容更新时会触发
>        console.log('hotmodule.js更新了');
>        let str = require('./hotmodule.js')
>        console.log(str)
>    })
>}
>```
>
>
>
>

## 4、webpack优化

>### 1、production模式打包自带优化
>
>+ tree shaking
>
> tree shaking是一个术语，通常用于打包时移除JavaScript中未引用的代码(dead-code),它依赖于ES6模块系统中`import`和`export`的静态结构特性。
>
> 开发时引入一个模块后，如果只使用其中一个功能，上线打包时只会把用到的功能打包金bundle，其他没用到的功能都不会打包进来，可以实现最基础的优化
>
>
>
>+ scope hoisting
>
> scope hoisting的作用是将模块之间的关系进行结果推测，可以让Webpack打包出来的代码更小、运行得更快
>
> scope hoisting的实现原理其实很简单：分析出模块之间的依赖关系，尽可能的把打散的模块合并到一个函数中去，但前提是不能造成代码冗余。
>
> 因此只有那些被引用了一次的模块才能被合并。
>
> 由于scop hoisting需要分析出模块之间的依赖关系，因此源码必须采用ES6模块化语句，不然它将无法生效。
>
> 原因和tree shaking一样。
>
>+ 代码压缩
>
> 所有代码使用UglifylsPlugin插件进行压缩、混淆
>
>### 2、CSS优化
>
>#### 2.1. 将css提取到独立文件中
>
>`mini-css-extract-plugin`是用于将css提取为独立的文件插件，对每个包含css的文件都会创建一个css文件，支持按需加载css和sourceMap
>
>只能用在webpack4中，有如下优势：
>
>+ 异步加载
>+ 不重复编译，性能更好
>+ 更容易使用
>+ 只针对css
>
>使用方法：
>
>1. 安装
>
>   `npm i -D mini-css-extract-plugin`
>
>2. 在webpack配置文件中引入插件
>
>   ```javascript
>   const MiniCssExtractPlugin = require('mini-css-extract-plugin')
>   ```
>
>3. 创建插件对象，配置抽离的css文件名，支持placeholder语法
>
>```javascript
>new MiniCssExtractPlugin({
>    filename:'[name].css'
>})
>```
>
>4. 将原来配置的所有`style-loader`替换为`MiniCssExtractPlugin.loader`
>
>   ```javascript
>   {
>       test:/\.css$/,
>           //webpack读取loader时，是从右到左读取，会将css文件先交给最右侧的loader来处理
>           //loader的执行顺序是从右到左以管道的方式链式调用
>           //css-loader：解析css文件
>           //style-loader:将解析出来的结果，放到html中，使其生效
>           //use:['style-loader','css-loader']
>           use:[MiniCssExtractPlugin.loader,'css-loader','postcss-loader']
>   }
>   //{test:/\.less$/,use:['style-loader','css-loader','less-loader']},
>   {test:/\.less$/,use:[MiniCssExtractPlugin.loader,'css-loader','less-loader']},
>       //{test:/\.s(a|c)ss$/,use:['style-loader','css-loader','sass-loader']},
>     {test:/\.s(a|c)ss$/,use:[MiniCssExtractPlugin.loader,'css-loader','sass-loader']}  
>   ```
>
>#### 2.2.自动添加css前缀
>
>使用`postcss`,需要用到`postcss-loader`和`autoprefixer`插件
>
>1. 安装
>
>   `npm i -D postcss-loader autoprefixer`
>
>2. 修改webpack配置文件中的loader,将`postcss-loader`放置在`css-loader`的右边(调用链从右到左)
>
>   ```javascript
>   {
>       test:/\.css$/,
>           //webpack读取loader时，是从右到左的读取，会将css文件先交给最右侧的loader来处理
>           //loader的执行顺序是从右到左以管道的方式链式调用
>           //css-loader：解析css文件
>           //style-loader:将解析出来的结果，放到html中，使其生效
>           //use:['style-loader','css-loader']
>           use:[MiniCssExtractPlugin.loader,'css-loader','postcss-loader']
>   }
>   //{test:/\.less$/,use:['style-loader','css-loader','less-loader']},
>   {test:/\.less$/,use:[MiniCssExtractPlugin.loader,'css-loader','postcss-loader','less-loader']},
>       //{test:/\.s(a|c)ss$/,use:['style-loader','css-loader','sass-loader']},
>       {test:/\.s(a|c)ss$/,use:[MiniCssExtractPlugin.loader,'css-loader','postcss-loder','sass-loader']}
>   ```
>
>3. 项目根目录下添加`postcss`的配置文件：`postcss.config.js`
>
>4. 在`postcss`的配置文件中使用插件
>
>   ```javascript
>   module.expots = {
>       plugins:[require('autoprefixer')]
>   }
>   ```
>
>#### 2.3.开启css压缩
>
>需要使用`optimiza-css-assets-webpack-plugin`插件来完成css压缩
>
>但是由于配置css压缩时会覆盖掉webpack默认的优化配置，导致JS代码无法压缩，所以还需要手动把JS代码压缩
>
>插件导入进来：`terser-webpack-plugin`
>
>1. 安装
>
>   `npm i -D optimize-css-assets-webpack-plugin terser-webpack-plugin`
>
>2. 导入插件
>
>```javascript
>const TerserJSPlugin = require('terser-webpack-plugin')
>const OptimizeCSSAssetsPlugin = require('optimize-css-assets-webpack-plugin')
>```
>
>3. 在webpack配置文件中添加配置节点
>
>```javascript
>optimization:{
>    minimizer:[new TerserJSPlugin({}),new OptimizeCSSAssetsPlugin({})],
>}
>```
>
>tips:webpack4默认采用的JS压缩插件为：`uglifyjs-webpack-plugin`,在`mini-css-extract-plugin`上一个版本中还推荐使用该插件，但最新的v0.6中建议使用`teser-webpack-plugin`来完成js代码压缩，具体原因在官网说明，我们就按照最新版的官方文档来做即可。
>
>### 3、JS优化
>
>Code Splitting 是webpack打包时用到的最重要的优化特性之一，此特性能够把代码分离到不同的bundle中，然后可以按需加载或并行加载这些文件，代码分离可以用于获取更小的bundle,以及控制资源加载优先级，如果使用合理，会极大影响加载时间。
>
>有三种常用的代码分离方法：
>
>+ 入口起点(entry points):使用`entry`配置手动地分离代码
>+ 防止重复(prevent duplication):使用`SplitChunksPlugin`去重复和分离chunk.
>+ 动态导入(dynamic imports):通过模块的内联函数调用来分离代码
>
>#### 3.1.手动配置多入口
>
>1. 在webpack配置文件中配置多个入口
>
>   ```javascript
>   entry:{
>       main:'./src/main.js',
>           other:'./src/other.js'
>   },
>       output:{
>           //path.resolve():解析当前相对路径和绝对路径
>           //path:path.resolve('./dist/'),
>           path:path.join(_dirname,'..','./dist/'),
>               //filename:'bundle.js',
>               filename:'[name].bundle.js',
>                   publicPath:.'/'
>       }
>   ```
>
>2. 在main.js和other.js中都引入了同一个模块，并使用其功能
>
>   main.js
>
>   ```javascript
>   import $ from 'jquery'
>   $(function(){
>       $('<div></div>').html('main').appendTo('body')
>   })
>   ```
>
>   other.js
>
>   ```javascript
>   import $ from 'jquery'
>   $(function(){
>       $('<div></div>').html('other').appendTo('body')
>   })
>   ```
>
>#### 3.2.抽取公共代码
>
>tips:Webpack  v4以上使用的插件为`SplitChunksPlugin`,以前使用的`CommonsChunkPlugin`已经被移除了，最新版的webpack只需要在配置文件中的`optimization`节点下添加一个`splitChunks`属性即可进行相关配置
>
>1. 修改webpack配置文件
>
>   ```javascript
>   optimization:{
>       splitChunks:{
>           chunks:'all'
>       }
>   }
>   ```
>
>2. 运行`npm run dev-build`重新打包
>
>3. 查看`dist`目录
>
>4. 查看`vendors~main~other.bundle.js`，其实就是把都用到Query打包到一个单独的js中
>
>#### 3.3.动态导入(懒加载)
>
>webpack4默认是允许import语法动态导入的，但是需要babel的插件支持，最新版babel的插件包为`@babel/plugin-syntax-dynamic-import`,以前老版本不是`@babel`开头，已经无法使用，需要注意动态导入最大的好处是实现了懒加载，用到哪个模块才会加载哪个模块，可以提高SPA应用程序首屏加载速度，Vue、React、Angular框架的路由懒加载原理一样
>
>1. 安装babel插件
>
>   `npm install -D @babel/plugin-syntax-dynamic-import`
>
>2. 修改.babelrc配置文件，添加`@babel/plugin-syntax-dynamic-import`插件
>
>   ```javascript
>   {
>   "presets":["@babel/env"],
>       "plugin":[
>           "@babel/plugin-proposal-class-properties",
>           "@babel/plugin-transform-runtime",
>           "@babel/plugin-syntax-dynamic-import"
>       ]
>   }
>   ```
>
>3. 将jQuery模块进行动态导入
>
>```javascript
> function getComponent(){
>    return import('jquery').then(({default:$})=>{
>        return $('<div></div>').html('main')
>    })
> }
>
>```
>
>4. 给某个按钮添加点击事件，点击后调用getComponent函数创建元素并添加到页面
>
>     ```javascript
>     window.onload = function(){
>         document.getElementById('btn').onclik = function(){
>             getComponent().then(item => {
>                 item.appendTo('body')
>             })
>         }
>     }
>     ```
>
>#### 3.4. SplitChunksPlugin配置参数
>
>webpack4之后，使用`SplitChunksPlugin`插件替代了以前`CommonsChunkPlugin`
>
>而`SplitChunksPlugin`的配置，只需要在webpack配置文件中的`optimization`节点下的`splitChunks`进行修改即可，如果没有任何修改，则会使用默认配置
>
>默认的`SplitChunksPlugin`配置适用于绝大多数用户
>
>webpack会基于如下默认原则自动分割代码：
>
>+ 公用代码块或来自node_modules文件夹的组件模块。
>+ 打包的代码块大小超过30k(最小化压缩之前)
>+ 按需加载代码时，同时发送的请求最大数量不应该超过5
>+ 页面初始化时，同时发送的请求最大数量不应该超过3
>
>以下是`SplitChunksPlugin`的默认配置
>
>   ```javascript
>   module.exports = {
>       optimization:{
>           splitChunks:{
>               chunks:'async',//只对异步加载的模块进行拆分，可选值还有all | initial
>               minSize:30000,//模块最少大于30KB都拆分
>               maxSize:0,//模块大小无上限，只要大于30KB都拆分
>               minChunks:1//模块最少引用一次才会被拆分
>               maxAsyncRequests:5,//异步加载时同时请求数量最大不能超过5，超过5的部分不拆分
>               maxInitialRequests:3,//页面初始化时同时发送的请求数量最大不能超过3，超过3的部分不拆分
>               automaticNameDelimiter:'~',//默认的连接符
>               name:true,//拆分的chunk名，设为true表示根据模块名和CacheGroup的key来自动生成，使用上面连接符连接
>               cacheGroups:{
>               //缓存组配置，上面配置读取完成后进行拆分，如果需要把多个模块拆分到一个文件，就需要缓存，所以命名为缓存组
>               vendors:{
>               //自定义缓存组名
>               test:/[\\/]node_modules[\\/]/, // 检查node_modules目录，只要模块在该目录下就使用上面配置拆分到这个组
>               priority:-10 //权重-10.决定了哪个组优先匹配，例如node_modules下有个模块要拆分，同时满足vendors和default组，此时就会分到vendors组，因为-10 > -20
>           },
>           default:{
>               //默认缓存组名
>               minChunks:2,//最少引用两次才会被拆分
>               priority:-20,//权重-20
>               reuseExistingChunk：true //如果主入口中引入了两个模块，其中一个正好也引用了后一个，就会直接复用无需引用两次
>           }
>           }
>           }
>       }
>   }
>   ```
>
>
>
>



