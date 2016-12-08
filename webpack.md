## webpack

>ģ������� & ������ߣ� ������¿ɲο�[��������-webpack](http://web.jobbole.com/tag/webpack/)��

### ��װ

```
npm install webpack -g --save
```

### ����

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

#### ���

```
/* entry: String | Array | Object */
entry:{
	name: ['a.js','b.js']
}

eg:
entry: [
	/*���ط���*/
	'webpack-dev-server/client?http://localhost:9090',
	/*����ļ�*/
	path.resolve(__dirname,'public/app.js')
]
```

#### ����

```
output: {
	/*����һЩ����·�������⣬��CDN*/
	publicPath: '',
	/*����ļ���·��*/
	path: path.resolve('public'),
	/*����ļ���[name](Ĭ��main)��[hash](�ļ���ϣֵ)*/
	filename: 'app/[name].min.js?[hash]'
}
```

#### ������

```
module: {
	loaders: [
		{ //es6������es5
			test: /\.js$/,
			exclude: /node_modules/,
			loader: 'babel'
		},
		{ //��ȡcss�ļ�
			test: /\.css$/,
			loader: ExtractTextPlugin.extract('style','css')
		}
	]
}
```

#### ���

```
plugins: [
	/*css�ļ���ȡĿ���ļ���[name](Ĭ��Ϊmain)*/
	new ExtractTextPlugin('[name].min.css')
]
```

### webpack���ò��

1. DefinePlugin ������������
```
plugins:{
	new webpack.DefinePlugin({
	   'process.env': {
	        NODE_ENV: '"development"'
	    }
	})
}
```
2. UglifyJsPlugin ѹ������
```
plugins:{
	new webpack.optimize.UglifyJsPlugin({
		mangle:{
			except: ['$','requires']
		}
	})
}
```
3. HotModuleReplacement �ȼ���
```
plugins:{
	new webpack.HotModuleReplacementPlugin()
}
```
4. ProvidePlugin ��ʱ����
```
plugins:{
	new webpack.ProvidePlugin({
		$: "jquery"
	})
}
```
5. DedupePlugin ɾ���ظ�����
```
plugins:{
	new webpack.optimize.DedupePlugin()
}
```
6. NoErrorsPlugin �����������
```
plugins:{
	new webpack.NoErrorsPlugin()
}
```
7. CommonsChunkPlugin ��ȡ����ģ��
```
plugins:{
	new webpack.optimize.CommonsChunkPlugin(options)
}
```
8. ExtractTextPlugin �ļ���ȡ
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
9. OpenBrowserPlugin ���������
```
var OpenBrowserPlugin = require('open-browser-webpack-plugin');
plugins:{
	new OpenBrowserPlugin({ url: 'http://localhost:9090/' })
}
```
10. HtmlWebpackPlugin HTML�ļ�����
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

### һ��������ʵ��

>���[����¹΢�̳�1.2��Ŀ](https://github.com/Scorain/JOBcoding/tree/master/yml/wechat1.2)


```
var webpack = require('webpack');
var path = require('path');
var OpenBrowserPlugin = require('open-browser-webpack-plugin');
var HtmlWebpackPlugin = require('html-webpack-plugin');
var ExtractTextPlugin = require("extract-text-webpack-plugin");

module.exports = {
	
    entry: [
	??? 'webpack-dev-server/client?http://localhost:9090',//��Դ��������ַ
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
                loader: 'url?limit=1024&name=img/[name].[ext]' // С��1k base64
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
        // �ȸ���
        new webpack.HotModuleReplacementPlugin(),
       	// �����������
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





