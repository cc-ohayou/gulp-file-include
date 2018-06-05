gulp-file-include
第一个我要介绍的是一个gulp的插件，他提供了一个include的方法让我们可以想后端模版一样把公共的部分分离出去。而且提供的include方法有许多配置项，详细可以去看看 gulp-file-include。

下面我们写一个小demo来快速的了解一下，我们需要先安装gulp以及gulp-file-include。

npm install -g gulp
mkdir gulp-file-include && cd gulp-file-include
npm install  gulp --save-dev
npm install gulp-file-include
安装好之后，来简单的组织一下文件的目录：

|-node_modules
|-src // 生产环境的 html 存放文件夹
    |-include // 公共部分的 html 存放文件夹
    |-*.html 
|-dist // 编辑后的 html 文件
gulpfile.js
在新建的gulpfile.js，配置好gulp-file-include：

var gulp = require('gulp');
var fileinclude  = require('gulp-file-include');

gulp.task('fileinclude', function() {
    gulp.src('src/**.html')
        .pipe(fileinclude({
          prefix: '@@',
          basepath: '@file'
        }))
    .pipe(gulp.dest('dist'));
});
接着新建两个html文件，分别是头部和底部：

header.html

<h1>这是 header 的内容</h1>
footer.html

<h1>这是 footer 的内容</h1>
最后在新建一个html，把要用到的header和footer给include进来。

layout.html

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
</head>
<body>
    @@include('include/header.html')

    <p> 这是 layout 的内容 </p>

    @@include('include/footer.html')
</body>
</html>
最后回到命令行工具里，执行gulp fileinclude


看到编译完成之后，到dist目录一下有一个layout.html的文件，这就是最后编译出来的。

好了，上面的一个小实例也明白之后。也许能够在以后的工作中大大提供生产力，使得自己写的html代码更加具有维护性和可复用性。