#Promise(承诺) 是一个有 then方法的对象

##Promise 的三种状态
```
    Fulfilled 成功状态
    Rejected失败的状态
    Pending   Promise对象实例创建时候的处置状态
    then 方法就是根据Promise对象的状态来确定执行操作  ，then方
        法可以使用链式操作就是因为每次执行总会返回一个Promise对象
```

#例子

```
    function readFile(filename){
        return new Promise(function(resolve,reject){
            require('fs').readFile(filename,'utf8',function(err,result){
                if(err){reject(err)}else{resolve(result)}
            })
          });
    }
    //第一种方法写        then()方法中有两个参数 data ,reason  
    readFile('11.txt').then(function(data){
        console.log('resolve'+data)
    },function(reason){
        console.log('reject'+reason)
    });
    
    
    //第二种方法写        then().catch() 
        readFile('1.txt').then(function(data){
            console.log('resolve'+data);
            return readFile(data);
        }).then(function(data){
            console.log('hh'+data);
        }).catch(function(reason){ // 捕获错误
            console.log(reason)
        });
```

#Promise.all
```
    Promise.all([p1,p2].then(function(result){
        console.log(result)
    }))
    不管两个promise谁先完成，Promise.all方法会按照数组里面的顺序将结果放回(两个状态？)
```

#Promise.race
```
Promise.race([p1,p2]).then(function(result){
        console.log(result)
})
    多个promise或者异步任务同时开始执行哪个先执行完就执行回调，并且把他的结果赋给result
```


#Q 
```
    Q把只提供回调函数方式的api封装成promise模式
    var Q=require('q');
    function fiveLater(){
        var defer= Q.defer();// 生成一个延迟对象
        setTimeout(function(){
            if(Math.random()>0.3){
                defer.resolve('成功');
            }else {
                defer.reject('失败');
            }
        },2000);
        return defer.promise;
    }

```



