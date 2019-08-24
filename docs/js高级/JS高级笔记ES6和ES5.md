## JS面向对象

* 面向对象：把任务分成一个一个的对象，由这些对象之间进行分工与合作

### 面向对象三大特性

* 封装性
* 继承性
* 多态性

## ES6的类和对象

类：抽象（泛泛）

* 1、抽取，把对象的属性和行为封装成一个类
* 2、对类进行实例化, 获取类的对象
* 3、类抽象了对象的公共部分，他泛指某一大类（class）
* 4、对象特指某一个，通过类实例化一个具体的对象

对象：具体

* 对象是由属性和方法组成的
* 对象有，类也有，从继承性继承过来的
* 属性和方法都不要前边的fuction

### 创建类

```js
语法：class 类名 {};

注意类名的首字母要大写

类要抽取公共属性方法，定义一个类，写在constructor () {}
```

### 类constructor构造函数

<u>构造函数的作用：接收参数，返回实例对象，主要放一些公共属性，new的时候主动执行,自动调用该方法</u>

> 注意：如果没有显示定义，类内部会自动给我们创建一个constructor()
>
> 注意：this代表当前实例化对象，谁new就代表谁
>
> new实力化    var ldh = new Preson ();   这里要带括号

### 添加类方法

```js
class 类名 { constructor(){}   方法名(){} }

注意：类中定义属性，调用方法都得用this
```

> 注意：方法之间不能加逗号分隔，同时方法不需要添加fuction关键字

### 类的继承

#### extends

```js
语法：

	class Father {}

	class Son extends Father{}

注意：是子类继承父类
```

#### super关键字

<u>super关键字用于访问和调用对象父类上的函数。可以调用父类的构造函数，也可以调用父类的普通函数</u>

**调用父类构造函数**

```js
class F { constructor(name, age){} }

class S extends F { 
  		constructor (name, age) {
			super(name,age); 
	}
}

注意: 子类在构造函数中使用super, 必须放到this 前面(必须先调用父类的构造方法,在使用子类构造方法
```

**调用父类普通函数**

```js
class F { 
  	constructor(name, age){} 
    say () {} 
}

class S extends F { 
  constructor (name, age) { 
    super(name,age); 
  } 
  	say () { 
      super.say() 
    } 
}
```

**总结：super调用父类的属性和方法，那么查找属性和方法的原则遵循就近原则**

#### 三个注意点

* 再ES6中没有变量提升，所以必须先定义类，才能通过类实例化对象
* 类里边的共有属性和方法一定要加this使用
* constructor里面this指向实例对象，方法里面的this指向这个方法的调用者

#### 类里边的this指向

- 构造函数的this指向实例对象
- 普通函数的this是调用者，谁调用，this是谁

#### 动态创建元素

* 现在高级做法:   利用insertAdjacentHTML() 可以直接把字符串格式元素添加到父元素中
* appendChild不支持追加字符串的子元素, insertAdjacentHTML支持追加字符串的元素
* insertAdjacentHTML(追加的位置,‘要追加的字符串元素’) 
* 追加的位置有: beforeend插入元素内部的最后一个子节点之后

```js
var li = '<li class="liactive"><span>' + neirong + '</span><span class="iconfont icon-guanbi"></span></li>';
// 直接把新创建的元素的结构拿过来，然后用insertAdjacentHTML进行插入

// beforeend指的是插入到后边
that.ul.insertAdjacentHTML('beforeend', li);
```



### 构造函数和原型

#### 创建对象可以通过下面三种方式

- 对象字面量

```js

var obj2 = {
    name: "小明",
    age: 20,
    sayHi:function () {
        console.log("我是：" + this.name);
    },
    eat:function () {
        console.log('吃了');
    }
```



- new Object()【构造函数】

```js
// var obj1 = new Object();
// obj1.name = name;
// obj1.age = age;
```

- 自定义构造 【this.yao = function () {}】

```js
function Gou (uname,age) {

		this.uname = uname;
		this.age = age;

		this.jiao = function () {
			console.log('汪汪叫');
		}

		this.tiao = function () {
			console.log('跳起来');
		}

	}

	var obj = new Gou('大黄',2);
	obj.jiao();
```



> instanceof : 运算符用来判断一个构造函数的prototype属性所指向的对象是否存在另外一个要检测对象的原型链上

> 修改标签属性：用qs获取之后，直接.src = b.jpg;



### 误区—tab案例

> 获取要点击的li的时候，要先获取大的div，通过它找到下边某一个具体div里边的li；

````js
this.mainTab = document.querySelector(id)
 // 获得要点击的li，这里获取的时候不用document，它获取的是页面上所有的li
// 用上边获取的tab，意思就是获取tab里的li
this.lis = this.mainTab.querySelectorAll('.fisrstnav li');
````

> 当点击的时候，注册一个点击事件

```js
// this.lis.onclick = function() {} 可以这样写，要是有10000个点击事件的话
// 就得有10000个函数，会占内存

// 这个this.toggleTab不加括号是要去找这个方法
this.lis[i].onclick = this.toggleTab;
单独给切换封装为一个方法
```

> 如何通过索引做匹配

```js
// 在这里加一个自定义属性，给他加上下标，通过索引找到对应的section
this.lis[i].index = i;
```

### 扩展

```js
tab栏案例：添加类名时，可以用
// this.classList.add('liactive');

也可以用
// this.className = 'liactive';
```



# JS高级第二天ES5

> 区分构造函数和普通函数

```
fuction fn () {}
fuction Fn () {}
```

* 用的时候有没有用new，得到的是一个对象
* 如果没有用的话,fn()就会返回undefined，因为没有return返回值

> new要干 的事

* 在内存中创建一个新的空对象。
* 让this指向这个新的对象【将构造函数里的this拿出来放到新的空对象里，也就是new新开辟的空间】
* 执行构造函数里面的代码，给这个新对象添加属性和方法
* 返回这个新对象，自带了一个return（所以构造函数里不需要return）



## 构造函数和原型

### 静态成员和实例成员

* 静态成员：不需要new，直接用的属性（属性也可以叫成员），只能由构造函数本身来访问。
* 实例成员：得new一个对象才能访问函数里的属性

```js
fuction Star (uname,age) {
	this.uname = uname;
	this.age = age;
}
var obj = new Star ();// 这个new出来的对象才可以访问到fuction这个函数里的属性（成员）

Star.score = 99;
这个不需要new就可以当访问到
console.log(Star.score);
```

**构造函数小问题**

```
当实例化对象的时候，方法是函数，函数是复杂数据类型
那么保存的时候是保存地址，又指向函数，而每创建一个对象，都会有一个函数，每个函数都得开辟一个新空间，浪费内存
```

### 构造函数原型prototype

> 原型对象就是一个属性，是构造函数的属性，这个属性是一个对象，也把prototype称为原型对象

**每一个构造函数都有一个prototype属性**

作用：为了共享方法，从而达到节省内存

> prototype是一个对象，这个对象的所有属性和方法，都会被构造函数所拥有。我们可以把那些不变的方法，直接定义在prototype对象上，这样所有的对象的实例就可以共享这些方法

**总结：所有的公共属性写道构造函数里面，所有的公共方法写到原型对象里面**

> 引出：为何创建一个对象，都可以自动的跑到原型对象上找方法，因为每一个对象都有一个属性，对象原型，执行原型对象

### 对象原型 ____proto____

* 主要作用：指向prototype

构造函数和原型对象都会有一个proto属性指向原型对象，之所以可以使用构造函数prototype原型对象的属性的方法，就是因为对象有proto原型的存在。

```js
注意：___proto___是一个非标准属性，不可以拿来赋值或者设置【只读属性】
```

* 构造函数.prototype == 实例化对象.proto
* proto对象原型和原型对象prototype是等价的
* proto对象原型的意义就在于对象的查找机制提供一个方向，但是他是一个非标准属性，所有在开发中，不可以使用这个属性，他只是指向原型对象prototype

> 总结：每一个对象都有一个原型，作用是指向原型对象prototype

### constuctor构造函数

> 指回构造函数本身

原型和构造函数原型对象里面都有一个constrcutor属性，constructor主要用于记录该对象引用哪个构造函数，他可以让原型对象重新指向原来的构造函数。

一般情况下，对象的方法都在对象原型中设置。

> 注意：如果有多个对象的方法，我们可以给原型对象采取对象形式赋值，但是这样就会覆盖构造函数原型对象原来的内容，这样修改后的原型对象constructor就不再指向当前构造函数了。此时，我们可以在修改后的原型对象中，添加一个constructor指向原来的构造函数。

```js
function Gou(uname, age) {

            this.uname = uname;
            this.age = age;
        }
        Gou.prototype = {
         // constructor: Gou,
            yao: function() {},

            jiao: function() {
                console.log('汪汪叫');
            },

            tiao: function() {
                console.log('跳起来');
            }
        }

        var obj = new Gou('大黄', 2);
        // console.log(obj.uname);
        // obj.jiao();
        // obj.tiao();
        console.log(Gou.prototype.constructor);

// 通过添加constructor: Gou这个，原型对象就可以指向Gou
```

### 构造函数、实例、原型对象三者之间的关系

![构造函数，原型对象，对象实例关系](D:\胡傲的翻身记录\JS高级\第一天\笔记\构造函数，原型对象，对象实例关系.jpg)

* prototype：原型对象，每一个构造函数都有这个属性
* proto：对象原型：每一个实例对象都有这个属性，这个属性的作用就是指向prototype
* contructor：构造函数，prototype，proto都有这个属性，这个属性的作用指回构造函数

**思考：如果传入一个对象给原型对象添加方法**

```js
Star.prototype = {
  
  	constructor: Star
  
 // 要加这一步，将它指回构造函数
  
    sing : function () {},
    dance: function () {}
};
此时会覆盖原来的prototype中的内容，传入一个新的对象，这时就不知道构造函数是哪个了

所以我们要只会构造函数：constructor：构造函数
```

### 原型链

- ![原型链](D:\胡傲的翻身记录\JS高级\第一天\笔记\原型链.jpg)


> 当给Object添加方法时，下边的子类实例对象都可以调用





### js的成员查找机制（规则）

````js
当访问一个对象的属性时，首先查找这个对象自身有没有该属性

如果没有就查找它的原型对象

如果还没有就在查找它原型对象的原型（object的原型对象）

一直找到object为止（null）

// console.log(Star.prototype.__proto__.__proto__);
// console.log(Object.prototype);
````

### 扩展内置对象

> 可以通过原型对象，对原来的内置对象进行扩展自定义的方法。比如给数组的求和的功能

```js
console.log( Array.prototype );
	// 添加求和方法
	Array.prototype.sum = function () {
		var sum = 0;
		for (var i = 0; i < this.length; i++) {
			sum += this[i];
		}
		return sum;
	}

	var arr = [1,2,3];
	console.log( arr.sum() );

	var newArr = [6,7,8,9];
	console.log( newArr.sum() );
```

### 继承

#### 属性的继承

```js
	function Father (uname,age) {
			// this指向父类的实例对象
			this.uname = uname;
			this.age = age;
			// 只要把父类的this指向子类的this既可
		}
		function Son (uname, age,score) {
			// this指向子类构造函数
			Father.call(this,uname,age);
			this.score = score;
		}
爸爸叫儿子过来，爸爸说我给你我的属性
		Son.prototype.sing = function () {
			console.log(this.uname + '唱歌')
		}
		var obj = new Son('刘德华',22,99);
		console.log(obj.uname);
		console.log(obj.score);
		obj.sing();
```

#### 方法的继承

实现方法：把父类的实例对象赋给子类的原型对象。

```js
 // new Father() = Son.prototype
```

> 如果直接将父类原型对象赋给子类的原型对象也可以实现，但是如果子类添加了新的方法，父类也会获得到

**注意：一定要让son指回构造函数**

```js
son.prototype.constructor = son;
```

### 类的本质

> 类的本质是一个函数
>
> 类的所有方法都定义在类的prototype属性上
>
> 类创建的实例，里面也有proto指向类的prototype原型对象

### ES5新增方法

#### 数组方法

```js
forEach()、filter()、some()
```



**forEach()**

```
array.forEach(function(ele,index))

ele：数组当前项的值
index：为数组的下标
```

**filter()—筛选**

```
array.filter(function(ele, index,arr))

返回一个新数组，所以要想得到新的数组，直接用一个变量去接收

ele为当前项的值
index为索引值
```

```js
var arr = [1,34,56,89];
var reArr = arr.filter(function(ele,index){
  return ele > 30;
  return ele % 2 == 0;
})

```

**some()—查找**

```js
array.some(function(ele,index));
【注意：找到满足的条件就停止循环】

注意：这个返回的是布尔值，如果查找到这个元素，就返回true，如果找不到就返回false

ele为当前项的值
index为索引值
```

```
var arr = [100,200,300,400];
var re = arr.some(function(ele,index){
  return ele >= 200;
  console.log(i)
})
console.log(re);
```

````js
这个是查找满足条件的索引值和当前值

var arr = [100, 200, 300, 400];
    var n;
    var re = arr.some(function(ele, index) {

        console.log(index);
        if (ele == 400) {
            n = ele;
            return true;
        }

    })
    console.log(n);
````





























