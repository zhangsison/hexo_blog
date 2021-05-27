---

title: webpack
date: 2019-12-06
categories: [web]
tags: [webpack]

---



## webpack


[webpack使用教程](https://github.com/poetries/mywiki/wiki/webpack)




> 安装全局依赖 webpack

	$ npm install -g webpack

安装webpack的时候 遇到的情况; 直接按照提示安装 提示Module webpack-cli 不存在
解决 npm install  webpack-cli -g


用 npm init 初始化项目

```bash
# 随便进一个目录

$ cd ~/codes

# 创建一个存放 webpack 项目的目录，名为 hello-webpack

$ mkdir hello-webpack

$ npm init

多出了一个名为 package.json

webpack.dev.config.js → 开发环境中用到的配置文件

webpack.pub.config.js → 生产环境中用到的配置文件

```

> 通过运行下面的命令进行配置文件的选择
```bash
webpack --config webpack.dev.config.js

配置npm的package.json文件

"scripts": {
	"test": "echo \"Error: no test specified\" && exit 1",
	"dev":"webpack --config webpack.dev.config.js",
	"pub":"webpack --config webpack.pub.config.js"
},

在根目录下执行命令

npm run dev

这样之后就不要敲那么复杂的命令了

```

**加载CSS**

> npm install --save-dev css-loader   style-loader
```bash

修改配置文件，在loaders中加上

{
	test: /\.css$/,
	loader: 'style!css' // 如果有多个加载器，中间用感叹号隔开，多个加载器从右往左执行
}

src/app.js 你可以为整个项目加载所有的 CSS

import  './project-styles.css';

```


图片处理

>下载依赖

```bash

npm  install  --save-dev url-loader file-loader

修改配置文件

{
test: /\.(png|jpeg|gif|jpg)$/,
loader: 'url?limit=25000'
}
```

## package.json文件 ##
```bash
var path = require('path');
module.exports = {
	entry: path.resolve(__dirname, 'src/js/app.js'),
	output: {
		path: path.resolve(__dirname, 'dist'),
		filename: 'bundle.js'
	},
	module: {
		loaders: [
			{
				test: /\.jsx?$/, 
				loader: 'babel',
				query: {
					presets: ['es2015', 'react']
				}
			},
			{
				test: /\.css$/, 
				loader: 'style!css' 
			},
			{
				test: /\.scss$/,
				loader: 'style!css!sass'
			},
			{
				test: /\.(png|jpeg|gif|jpg)$/,
				loader: 'file-loader?name=images/[name].[ext]'
			},
		]
	},
}

```

# 常用插件介绍 #
> 压缩插件

```js
这个插件是webpack自带的

// 用webpack压缩代码，可以忽略代码中的警告
new webpack.optimize.UglifyJsPlugin({
	compress: {
		warnings: false
	}
}),

```

- CSS插件

> npm install --save-dev extract-text-webpack-plugin

```js
	使用
// 可以新建多个抽离样式的文件，这样就可以有多个css文件了。
new ExtractTextPlugin("app.css"),

plugins: [
	// 可以新建多个抽离样式的文件，这样就可以有多个css文件了。
	new ExtractTextPlugin("app.css"),
]

修改loaders中的配置：
{
	test: /\.css$/,
	loader: ExtractTextPlugin.extract('style-loader' , 'css-loader')
},
```


- html页面插件


> npm install --save-dev html-webpack-plugin 

使用

```js
// 自动生成index.html页面插件
var HtmlWebpackPlugin = require('html-webpack-plugin');
plugins: [
	new HtmlWebpackPlugin({
		template: './src/template.html',
		htmlWebpackPlugin: {
			"files": {
				"css": ["app.css"],
				"js": ["vendors.js","bundle.js"]
			}
		},
		minify: {
			removeComments: true,
			collapseWhitespace: true,
			removeAttributeQuotes: true
		}
	}),
]
```


- 删除插件

> npm install --save-dev clean-webpack-plugin

```js
// 删除文件夹
var CleanPlugin = require('clean-webpack-plugin');

plugins: [
	// 构建之前先删除dist目录下面的文件夹
	new CleanPlugin(['dist']),
]
```


- 去掉react中的警告

```js
plugins: [
	new webpack.DefinePlugin({
		//去掉react中的警告，react会自己判断
		'process.env': {
			NODE_ENV: '"production"'
		}
	}),
]
```


# 常见问题 #
> 输入npm install webpack --save-dev 

**局部安装webpack提示无法依赖**
	npm ERR！ Windows_NT 6.1.7601 
说明你执行命令的目录里有一个package.json文件，并且该文件里的name字段就叫webpack。换个名字就好了




# webpack 插件 #
**学习插件的第一步，是进入其主页，先把它的 readme 文档看看，至少知道它是干什么的，能解决什么问题，最后知道如何用就行了**
