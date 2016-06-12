#gulp
```
gulp是可以自动化执行任务的工具（主要重复动作）
    1.把一个文件拷贝到另个一位置
    2.把多个JS或者CSS文件合并成一个文件并压缩
    3.把Sass或者Less文件编译成CSS
    4.压缩图像文件以减少网络流量
    5.创建一个可以实时刷新页面内容的本地服务器
```

##gulp安装
```
    全局安装 npm install -g gulp   -->可以在命令行中使用
    本地安装并增加开发依赖  npm install gulp --save-dev     ----->当前文件需要还得require进来
             从本地的node_modules中查找，如果找不到向上级查找，如果一直到根目录 都没有找到，就报错
    
```


##gulp任务创建
```
   1.gulp.task('hello',function(){})  --->创建gulp任务 名字为hello    (在命令行中运行  gulp hello)
   2.运行gulp的文件名必须为gulpfile.js  如果是其他名就会报错

```

##gulp 四个api(task/src/watch/dest/)
```
    1.task-->创建任务 gulp.task('hello',[依赖任务],fn)  fn为把任务要执行的代码都写在里面 
    2.src-->源地址gulp.src('路径',{可以配置base参数})  
    3.watch  监控的对象 当对象发生变化执行回调函数 
    4.dest--->gulp.dest(path)-->path要写入的路径,(path+gulp.src()中有通配符开始出现的那部分路径)
```

```
gulp.task('copy',function(){
        return gulp.src(['app/**/*.css','app/**/*.js','!app/**/*.tmp.js'],{base:'app'})
    .pipe(gulp.dest('dist'))});
```

##gulp插件
```
    gulp-load-plugins:自动加载package.json文件里的gulp插件
    var gulp=require('gulp');
    var $ =require('gulp-load-plugins')();
    
    var concat=require('gulp-concat'); 把几个文件合并到一块
    gulp.task('concat',function(){   
        return gulp.src(['app/**/*.js','!app/**/*.tmp.js'])  //指定要合并的文件
        .pipe(concat('app.js'))  //进行合并并指定合并后的文件名
        .pipe(gulp.dest('dist/js'))  //输出到目标路径
    });
```

#watch
```
    // 参数一 是指要监控的对象
    // 参数二 当文件发生变化的时候执行的回调函数
    gulp.watch('./src1/index.html',function(event){
        console.log(event);
        //type  表示变化的类  changed改变    added新增    deleted删除
        //path  变化的文件
    
    });
```


#