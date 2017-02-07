## webpack

>模块加载器 & 打包工具， 相关文章可参考[伯乐在线-webpack](http://web.jobbole.com/tag/webpack/)。

### 安装

```
npm install webpack -g --save
```

### 配置

```
var webpack = require('webpack');
var path = require('path');
var ExtractTextPlugin = require("extract-text-webpack-plugin");
module.exports = {
	entry: {},
	output: {},
	module: {},
	resolve: {},
	plugins: {}
}
```

#### 入口

```
/* entry: String | Array | Object */
entry:{
	name: ['a.js','b.js']
}

eg:
entry: [
	/*本地服务*/
	'webpack-dev-server/client?http://localhost:9090',
	/*入口文件*/
	path.resolve(__dirname,'public/app.js')
]
```

#### 出口

```
output: {
	/*处理一些引用路径的问题，如CDN*/
	publicPath: '',
	/*输出文件的路径*/
	path: path.resolve('public'),
	/*输出文件名[name](默认main)、[hash](文件哈希值)*/
	filename: 'app/[name].min.js?[hash]'
}
```

#### 加载器

```
module: {
	loaders: [
		{ //es6编译至es5
			test: /\.js$/,
			exclude: /node_modules/,
			loader: 'babel'
		},
		{ //提取css文件
			test: /\.css$/,
			loader: ExtractTextPlugin.extract('style','css')
		}
	]
}
```

#### 插件

```
plugins: [
	/*css文件提取目标文件名[name](默认为main)*/
	new ExtractTextPlugin('[name].min.css')
]
```

### webpack常用插件

1. DefinePlugin 开发环境定义
```
plugins:{
	new webpack.DefinePlugin({
	   'process.env': {
	        NODE_ENV: '"development"'
	    }
	})
}
```

2. UglifyJsPlugin 压缩混淆
```
plugins:{
	new webpack.optimize.UglifyJsPlugin({
		mangle:{
			except: ['$','requires']
		}
	})
}
```

3. HotModuleReplacement 热加载
```
plugins:{
	new webpack.HotModuleReplacementPlugin()
}
```

4. ProvidePlugin 即时加载
```
plugins:{
	new webpack.ProvidePlugin({
		$: "jquery"
	})
}
```

5. DedupePlugin 删除重复依赖
```
plugins:{
	new webpack.optimize.DedupePlugin()
}
```

6. NoErrorsPlugin 跳过编译错误
```
plugins:{
	new webpack.NoErrorsPlugin()
}
```

7. CommonsChunkPlugin 提取公共模块
```
plugins:{
	new webpack.optimize.CommonsChunkPlugin(options)
}
```

8. ExtractTextPlugin 文件抽取
```
var ExtractTextPlugin = require("extract-text-webpack-plugin");
module:{
	loaders: [
		{
			test: /\.**$/,
			loader: ExtractTextPlugin.extract([notExtractLoader], loader, [options])
		}
	]
}
plugins:{
	new ExtractTextPlugin([id: string], filename: string, [options])
}
```

9. OpenBrowserPlugin 启动浏览器
```
var OpenBrowserPlugin = require('open-browser-webpack-plugin');
plugins:{
	new OpenBrowserPlugin({ url: 'http://localhost:9090/' })
}
```

10. HtmlWebpackPlugin HTML文件生成
```
var HtmlWebpackPlugin = require('html-webpack-plugin');
plugins:{
	new HtmlWebpackPlugin({
        template: './public/index-async.html',
	    filename: './index.html',
	    inject: 'body'
    })
}
```

### 一个完整的实例

>另见[友门鹿微商城1.2项目](https://github.com/Scorain/JOBcoding/tree/master/yml/wechat1.2)


```
var webpack = require('webpack');
var path = require('path');
var OpenBrowserPlugin = require('open-browser-webpack-plugin');
var HtmlWebpackPlugin = require('html-webpack-plugin');
var ExtractTextPlugin = require("extract-text-webpack-plugin");

module.exports = {
	
    entry: [
	??? 'webpack-dev-server/client?http://localhost:9090',//资源服务器地址
	??? path.resolve(__dirname, 'public/app.js'),
	],
	output: {
		publicPath: '',//cdn
        path: path.resolve('public'),
        filename: 'app/[name].min.js?[hash]'
	},
	module: {  
		loaders:[
            {
                test: /\.js$/,
                exclude: /node_modules/,
                loader: 'babel'
            }, 
            {
                test: /\.(png|jpg|gif)$/,
                loader: 'url?limit=1024&name=img/[name].[ext]' // 小于1k base64
            },
            {
            	test: /\.css$/, 
            	loader: ExtractTextPlugin.extract("style", "css")
            	//loader: "style-loader!css-loader?modules"
            },
            {
                test: /\.less$/,
                loader: ExtractTextPlugin.extract("style", "css!less")
                //loader: "style-loader!css-loader?modules"
            },
            {
			   test: /\.html$/,
			   loader: "raw-loader"
			}
        ]
	},
	resolve:{
		alias: {
	        /*angular: "/node_modules/angular/angular"*/
	    }
	},
	plugins:[
		new webpack.DefinePlugin({
	      'process.env': {
	        NODE_ENV: '"development"'
	      }
	    }),
        new OpenBrowserPlugin({ url: 'http://localhost:9090/' }),
        // 热更新
        new webpack.HotModuleReplacementPlugin(),
       	// 打包第三方库
        // new webpack.optimize.CommonsChunkPlugin({
        //     names: ['common'],
        // }),
        // replace static 
        new HtmlWebpackPlugin({
	        template: './public/index-async.html',
	        filename: './index.html',
	        inject: 'body'
	    }),
	    // mincss
	    new ExtractTextPlugin("[name].min.css"),
	    // new webpack.optimize.UglifyJsPlugin({
	    //   compress: {
	    //     warnings: false
	    //   }
	    // })
	]
}; 

```





