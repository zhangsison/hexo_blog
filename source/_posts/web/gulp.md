---

title: gulp
date: 2019-07-06
categories: [web]
tags: [gulp]

---


## gulp

![](https://lc-gold-cdn.xitu.io/525072a07f737c146231.png?imageView2/1/w/1304/h/734/q/85/interlace/1)
## gulp ##
[gulp](https://gulpjs.com/)是一个自动化工具,搭建web服务器,文件保存时自动重载浏览器,合并文件、压缩代码、检查语法错误、将Sass代码转成CSS代码等等,可以帮助我们自动管理和运行各种任务

## gulp安装 ##
先安装Node.js npm


> 官方示例
> 
> npm install gulp-cli -g
> 
> npm install gulp -D
> 
> npx -p touch nodetouch gulpfile.js
> 
> gulp --help


## 创建Gulp项目 ##

首先，我们新建一个文件夹，并在该目录下执行npm init命令

> npm init

npm init命令会为你创建一个package.json文件，这个文件保存着这个项目相关信息。

## gulpfile.js ##

项目根目录下创建一个名为 gulpfile.js 的文件，此文件为gulp的配置文件

```
var gulp = require('gulp'),//基础库
htmlmin = require('gulp-htmlmin'),//html压缩
uglify = require('gulp-uglify');
clean = require('gulp-clean-css');
imagemin = require('gulp-imagemin');
rename = require('gulp-rename');
concat = require('gulp-concat');


​	 
​	
// 压缩js
gulp.task('htmlcompress', function () {
return gulp.src('*.html')
.pipe(htmlmin())
.pipe(gulp.dest('/www/yasuo/ya/'))
})


​	
// 压缩js
gulp.task('jscompress', function () {
return gulp.src('js/*.js')
.pipe(uglify())
.pipe(gulp.dest('/www/yasuo/ya/js'))
})

// 压缩css
gulp.task('csscompress', function () {
return gulp.src('css/*.css')
.pipe(clean())
.pipe(gulp.dest('/www/yasuo/ya/css'))
})

// 压缩image
gulp.task('imagecompress', function () {
return gulp.src(['images/*.jpg', 'images/*.png'])
.pipe(imagemin())
.pipe(gulp.dest('/www/yasuo/ya/images'))
})

// 合并js
gulp.task('concatJs', function () {
return gulp.src('js/index.js')
.pipe(concat('concat.js'))
.pipe(gulp.dest('/www/zhuanpan/ya/js'))
})

// 监听js和css的改动
gulp.task('auto', function () {
gulp.watch('js/*.js', ['jscompress']);
gulp.watch('css/*.css', ['csscompress']);
})

// 默认任务
gulp.task('default', ['jscompress', 'csscompress', 'imagecompress', 'concatJs', 'htmlcompress']);

// gulp.task('default', [ 'csscompress', 'imagecompress',  'htmlcompress']);

```

## 常用插件 ##
```
gulp-load-plugins：自动加载 package.json 中的 gulp 插件，避免一个个require插件
gulp-rename： 重命名
gulp-uglify：文件压缩
gulp-concat：文件合并
gulp-less：编译 less
gulp-sass：编译 sass
gulp-clean-css：压缩 CSS 文件
gulp-htmlmin：压缩 HTML 文件
gulp-babel: 使用 babel 编译 JS 文件
gulp-jshint：jshint 检查
gulp-imagemin：压缩jpg、png、gif等图片
gulp-livereload：当代码变化时，它可以帮我们自动刷新页面，除在模块中需要安装外，还需要在浏览器中安装。
gulp-csso 压缩优化css
gulp-html-minify压缩HTML
gulp-imagemin压缩图片
gulp-zip ZIP压缩文件
gulp-base64将css文件里引用的图片转为base64
```
[插件下载地址](https://gulpjs.com/plugins/)

## 流程控制 ##
```
- run-sequence - 按照顺序执行task (注意: 在 Gulp4.0 中, 已经提供了 gulp.series 方法)


- gulp-if - If-Else-流程控制


- gulp-ignore - 选择性过滤文件


- gulp-filter - 过滤文件, 和 gulp-ignore感觉类似


- merge-stream - Merge multiple streams into one interleaved stream.


- event-stream - 方便操作stream


- gulp-plumber - Prevent pipe breaking caused by errors.


- gulp-notify - 系统通知


- gulp-changed - 只通过修改过的文件


- gulp-changed-in-place - 只通过修改过的文件
区别? 


- gulp-changed 比较的是生成的文件, gulp-changed-in-place比较的是源文件, 复杂情况用后者. (比如需要babel的时候)


- gulp-order - 重新对文件进行排序 (引入顺序重要的话, 这个插件结合 event-stream 是神器)
```

## gulp的API ##

使用gulp，仅需知道4个API即可：**gulp.task(),gulp.src(),gulp.dest(),gulp.watch()**，所以很容易就能掌握。为了避免出现理解偏差，建议先看一遍官方文档
https://www.gulpjs.com.cn/docs/api/


## 匹配符 *、**、！、{} ##
```

gulp.src('./js/*.js')               // * 匹配js文件夹下所有.js格式的文件
gulp.src('./js/**/*.js')            // ** 匹配js文件夹的0个或多个子文件夹
gulp.src(['./js/*.js','!./js/index.js'])    // ! 匹配除了index.js之外的所有js文件
gulp.src('./js/**/{omui,common}.js')        // {} 匹配{}里的文件名
```
## 文件操作 ##
```
var del = require('del');

del('./dist');                      // 删除整个dist文件
```
## gulp-rename重命名文件 ##
```
var rename = require("gulp-rename");

gulp.src('./hello.txt')
.pipe(rename('gb/goodbye.md'))    // 直接修改文件名和路径
.pipe(gulp.dest('./dist')); 

gulp.src('./hello.txt')
.pipe(rename({
dirname: "text",                // 路径名
basename: "goodbye",            // 主文件名
prefix: "pre-",                 // 前缀
suffix: "-min",                 // 后缀
extname: ".html"                // 扩展名
}))
.pipe(gulp.dest('./dist'));

```
## gulp-concat合并文件 ##
```
var concat = require('gulp-concat');

gulp.src('./js/*.js')
.pipe(concat('all.js'))         // 合并all.js文件
.pipe(gulp.dest('./dist'));

gulp.src(['./js/demo1.js','./js/demo2.js','./js/demo2.js'])
.pipe(concat('all.js'))         // 按照[]里的顺序合并文件
.pipe(gulp.dest('./dist'));
```

# gulp自动化压缩合并、加版本号解决方案 #


> 主要是为了实现js/css的压缩合并、自动添加版本号和压缩html。
```
gulp-csso 压缩优化css
gulp-uglify 压缩js
gulp-html-minify 压缩html
gulp-rev-all 生成版本号
```


> 主要通过上面插件实现功能，其他插件配合使用。
```
// gulpfile.js
var gulp = require('gulp'),
htmlmini = require('gulp-html-minify'),
useref = require('gulp-useref'),
uglify = require('gulp-uglify'),
csso = require('gulp-csso'),
filter = require('gulp-filter'),
RevAll = require('gulp-rev-all'),
del = require('del');

gulp.task('default',['del'], function () {
var jsFilter = filter('**/*.js',{restore:true}),
cssFilter = filter('**/*.css',{restore:true}),
htmlFilter = filter(['**/*.html'],{restore:true});
gulp.src('/*.html')
.pipe(useref())                         // 解析html中的构建块
.pipe(jsFilter)                         // 过滤所有js
.pipe(uglify())                         // 压缩js
.pipe(jsFilter.restore)
.pipe(cssFilter)                        // 过滤所有css
.pipe(csso())                           // 压缩优化css
.pipe(cssFilter.restore)
.pipe(RevAll.revision({                 // 生成版本号
dontRenameFile: ['.html'],          // 不给 html 文件添加版本号
dontUpdateReference: ['.html']      // 不给文件里链接的html加版本号
}))
.pipe(htmlFilter)                       // 过滤所有html
.pipe(htmlmini())                       // 压缩html
.pipe(htmlFilter.restore)
.pipe(gulp.dest('/dist'))
})

gulp.task('del',function () {
del('/dist');                               // 构建前先删除dist文件里的旧版本
})

```

> 在html中，先定义好构建块。
```
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>gulp自动化构建解决方案</title>
<!-- build:css static/css/index.css -->     // 定义了构建后引用的css路径
<link rel="stylesheet" href="static/css/common.css"/>
<link rel="stylesheet" href="static/css/index.css"/>
<!-- endbuild -->
</head>
<body>
......

<!-- build:js static/js/index.js -->        // 定义了构建后引用的js路径
<script src="static/js/jquery.js"></script>
<script src="static/js/common.js"></script>
<script src="static/js/index.js"></script>
<!-- endbuild -->
</body>
</html>
```


> 执行构建完成后，会生成 dist 文件夹，目录
```
|-dist
|   |-static
|       |-css
|           |-index.96cf44da.css
|       |-js
|           |-index.42ce3282.js
|   |-index.html
```


> 构建完的index.html，我们忽略压缩的html，完成了压缩合并添加版本号等功能。
```
// dist/index.html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>gulp自动化构建解决方案</title>
<link rel="stylesheet" href="static/css/index.96cf44da.css"/>
</head>
<body>
......

<script src="static/js/index.42ce3282.js"></script>
</body>
</html>
```