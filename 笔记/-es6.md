#es6 常用操作

```
   let     let a=1; //块级作用域
   const      const PI=3.22;  //常量一旦被定义便不能再修改
    
```

###箭头函数（简化了函数的定义方式）  =>
```
    左边为输入，右边是进行的操作以及返回的值
    如果输入的参数多于1个，需要用小括号括起来
    如果不只是一个简单的输出需要大括号把语句括起来
    var add = (val1,val2) => {};
    console.log(add(1,2));
    
    
    //箭头函数没有自己的this,而会和上级共用this对象
    var person = {
        start:function(){
            console.log(this);
            //var self = this;
            //箭头函数没有自己的this,而会和上级共用this对象
            setTimeout(()=>{
                console.log(this);
            },1000)
        }
    }
```

##对象字面量
```
    定义方法可以不用function关键字
    可以在对象字面量里面指定此对象的原型，从而直接调用父类方法
    var person={
        eat(){
            console.log('hh');
        }
    };
    var teacher={
        __proto__:person,
        teach(){
            console.log('ok')
        }
    };
    teacher.eat();
    teacher.teach();
```

##解构赋值 (数组、对象)
```
        //对象的解构赋值
        var obj = {name: 'zfpx', age: 8};
        var {name,age} = obj;
        
        console.log(name, age);
        
        //数组的解构赋值
        var arr = [1, 2, 3];
        let [a,b] = arr;
        console.log(a, b);
        
        
        
        
        var name = 'zfpx';
        var age = 8;
        //console.log(`${name} is ${age} years old!`)
        //// ZFPX IS 8 YEARS OLD!
    function uppercase(strings,...values){
        //console.log(strings);
        //console.log(values);
        //用变量把字符串进行拆分 变量的数组长的长度+1= 字符串数组长度
        var str = '';
        for(var i=0;i<values.length;i++){
            str += (strings[i]+values[i]).toUpperCase();
        }
        str += strings[i].toUpperCase();
        console.log(str);
    }
    console.log(`${name} is ${age} years old!`);
    //带标签的模板字符串
    uppercase`${name} is ${age} years old!`

    
```
###默认参数和...
```
    //默认参数
    function ajax(url = '/', method = 'get') {
        console.log(method, url);
    }
    ajax('/ajax', 'post');
    
    
    //把其它的剩余参数转成一个数组赋给numbers
    function show(prefix, ...numbers) {
        //var result = Array.prototype.slice.call(arguments,1).reduce((a,b)=>a+b);
        // from 用于把一个类数组转成数组
        //console.log(Array.from(arguments));
        //var result = Array.from(arguments).slice(1).reduce((a,b)=>a+b);
        var result = numbers.reduce((a, b)=>a + b);
    
        console.log(prefix + ':' + result);
    }
    show('结果', 2, 3, 4);
```
###合并对象
```
    var target = {a: 1};
    var sourceb = {b: 2};
    var sourcec = {c: 3};
    /*for(var attr in sourceb){
     target[attr] = sourceb[attr];
     }
     for(var attr in sourcec){
     target[attr] = sourcec[attr];
     }*/
    Object.assign(target, sourceb, sourcec);
    console.log(target);
```

##then方法深入
```
    //then源码
    
    module.exports = {
        defer:function() {
            var success,fail,val,error;
            return {
                resolve:function(data){
                    val = data;
                    if(success)
                    success(val);
                },
                reject:function(reason){
                    error = reason;
                    if(fail)
                    fail(error);
                },
                promise:{
                    then:function(fullfilled,rejected){
                        if(val){
                            fullfilled(val);
                        }else{
                            success = fullfilled;
                        }
                        if(error){
                            rejected(error);
                        }else{
                            fail = rejected;
                        }
                    }
                }
            }
        }
    }
    
    //引用
    
    var Q = require('./q');
    var defer = Q.defer();//延迟的任务
    setTimeout(function () {
        if (Math.random() > 0.5) {
            defer.resolve('成功');
        } else {
            defer.reject('失败');
        }
    },1000);
    var promise = defer.promise;
    
    setTimeout(function(){
        promise.then(data=> {
            console.log(data);
        }, (reason) => {
            console.error(reason);
        });
    },3000);
   
```

##reduce方法
```
    var addAll = function(){
        // from可以把类数组转成数组
        return Array.from(arguments).reduce(
            function(current,next){
                return current>next?current:next;
            },0);
    }
    
    console.log(addAll(1,2,3));

```