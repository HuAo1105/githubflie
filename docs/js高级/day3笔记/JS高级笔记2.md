change一般加在输入框和文本域中

form有三个属性   name   

​				提交到哪  action

## 去除空白符：

* trim()这个只能去除字符串左右两边的空格
* 先用split切割字符串，返回一个数组
* 再用jion把一个一个数组拼接成字符串

```js
var str = ' aas ase azx ';
	// console.log(str);
	// 返回： aas ase azx 

    // 注意上边
var arr = str.split(' ');
    // console.log(arr);
	// 返回：["", "aas", "ase", "azx", ""]
str = arr.join('');
// 就是将原来有空格的地方化为无空格
// console.log(str);
// 返回：aasaseazx
```

## 函数的定义和调用

### 函数表达式

```js
var fn = function() {
        console.log(1223);
    }
fn();
var fn = function(a,b) {
        return a+b
    }
fn(1,2);
```

### 自调用函数

```
(function(a,b){
  return a+b;
})(1,2);
```

> 函数也是一个对象

### 函数调用方式

```
1、普通函数
2、对象的方法
3、构造函数
4、绑定事件函数
5、定时器函数
6、立即执行函数==>自调用函数
```

## this指向

this：当前调用者

* 普通函数调用  == >   window
* 构造函数调用  == >   实例对象  原型对象里面的方法也指向实例函数
* 对象方法调用  == >    该方法所属对象
* 事件绑定方法  == >     绑定事件对象
* 定时器函数      == >     window
* 立即执行函数   == >     window



> 非定时器代码会优先于定时器代码执行







## call、apply、bind改变函数this指向

* 都是改变this的指向
* apply传入参数的时候，要用数组的形式
* bind和call一样，不用数组，但是bind不会调用，需要一个变量来接收，然后这个变量就成了一个函数，然后【函数()】来调用。

### call

```js
function father  (参数1，参数2)   {this};
function Son ()   {
  Father.call(this,arg1,arg2);
}
 arg1,arg2  为传入的参数
 还有就是call经常做继承
```

### apply

```js
fun.apply(obj,[a,b,c]);
这个传入形参的时候要以数组的形式传入
```

> 借助于apply来求最大值

```js
var arr = [1,2232,343];
var n = Math.max.apply(null,arr);

这个没有要改变的this，只是求数组的最大值，所以写null，也可以写Math本身；

因此apply主要和数组有关系
```

### bind

```js
fun.bind(thisarg,arg1,arg2);
arg1,arg2  为传入的参数

bind不调用函数，但是还想改变this指向，比如改变定时器内部的this指向

var input = document.querySelector('input');
    input.onclick = function() {

        this.disabled = true;

         window.setTimeout(function() {

         this.disabled = false;

       }.bind(this), 2000);
   }
    
    
******bind(this)的这个this指向btn，所以就把window里的this改变指向了btn*******
      ******这样以后就可以只改变注册的事件就可以了*******      
      
function() {this.disabled = false;}   这个函数本身就是一个对象，所以直接在后边调用bind即可，把函数内部的this想指向谁把谁写在括号里
```



## 严格模式

> js分为正常模式和严格模式

开启严格模式："use strict";

可以在整个脚本开启和函数内开启

## 高阶函数

```
高阶函数是对其他函数进行操作的函数，它接收函数作为参数或将函数作为返回值输出
```

```js
此时fn就是一个高阶函数

函数也是一种数据类型，同样可以作为参数，传递给另外一个参数使用。最典型的就是作为回调函数

同理 函数也可以作为返回值传递回来

function fun (lilei) {
  lilei();
};
fun (function() {
  console.log('你好')
});

lilei ==> function() {console.log('你好')};后边的函数作为实参传给lilei，然后它再调用



function fun() {
            return function() {
                console.log('函数');
            };
        }
 fun()();

// fun() = ƒunction () {console.log('函数');}

所以fun()这会还是一个函数，要再加一个()调用执行
```

## 闭包

```
变量根据作用域的不同分为两种：全局变量和局部变量

1、函数内部可以使用全局变量
2、函数外部不可以使用局部变量
3、当函数执行完毕，本作用域内的局部变量会销毁
```

### 什么是闭包

闭包作用：延伸变量的作用范围

```js
闭包：简单理解就是，一个作用域可以访问另外一个函数的局部变量

function fn1() {
  // fn1就是闭包函数
  var num = 10;
  function fn2 () {
    console.log(num);
  }
  fn2(); 
  // 执行fn2的时候，发现找不到num变量，就会向上找
}
fn1();
```

**在函数外边访问到函数内部的变量**

```js
 function fn() {
        var i = 7;

        return function() {
            console.log(i);

        }
    }
 fn()();

// 直接将内部的函数return出来，所以执行的时候fn()还是一个函数要在加一个();
```

**练习:**

```js
注册事件练习：打印索引值
var lis = document.querySelectorAll('li');

	for (var i = 0; i < lis.length; i++) {

		(function (index) {
			lis[index].onclick = function () {
				console.log(index);
			}
		})(i);
}
```



# 第四天

## 递归

* 递归就是函数自己调用自己

return在函数里后边不写返回的是undefined

函数执行完要返回给调用者【原位置】

> 加入一个数组下有好多对象，对象下边有好多数组，想要找这里边的东西，遍历

```js
var data = [{
        id: 1,
        name: '家电',
        goods: [{
            id: 11,
            gname: '冰箱',
            goods: [{
                id: 111,
                gname: '海尔'
            }, {
                id: 112,
                gname: '美的'
            }, ]
        }, {
            id: 12,
            gname: '洗衣机'
        }]
    }, {
        id: 2,
        name: '服饰'
    }];
    // 这里传入两个参数，一个是哪一个数组，还有一个是id
    function fn(data, id) {
        var newobj = {};
        data.forEach(function(ele, i) {
            if (ele.id == id) {
                newobj = ele;
            } else if (ele.goods && ele.goods.length > 0) {
                newobj = fn(ele.goods, id);
            }
        });
        return newobj;
    }
console.log(fn(data, 11));

现在想要给
```





## 不知道的



<input type = '"text" readonly = "readonly">

* readonly为只读，不能在输入框输入
* disabled为禁用








for in 遍历对象的时候，获取属性的时候不要用obj.name;要用obj['name'];因为obj.name可能被认为是obj对象里的属性



拷贝不能直接赋值，是共享的一个地址，如果前一个值改变的话，复制的那个也会变。



浅拷贝只能拷贝外层的{}

函数  数组    对象都是复杂类型

instanceof判断是不是想要的类型，返回的是布尔值



BOM里的一个对象：location，有一个属性：href

location.href = "http://www.baidu.com"



提交事件：onsubmit



继承属性时，用call和apply，bind可以改变this的指向，但是不执行函数函数，要是用也可以，要这样写，后边加一个括号就执行了

```js
//   Star.bind(this, uname, age)();
```



继承方法时，要先把new Father () = Son.prototype，这句话写在前边，然后再改变子类的构造函数的指向，再去对子类实例对象，再去调用

