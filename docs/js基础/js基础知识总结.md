### js对象

* 引用类型
  * object、array、date、RegExp、Function
* 基本包装类型
  * boolean、number、string
* 内置对象
  * Global、Math

### js操作符

* 比较操作符 优先级高于 赋值操作符
* 字符串遇见其他（- * / %）：隐式转化为数字类型

#### 逻辑运算符

* && 且 ：全部满足 
  * 常规：需要Boolean值进行逻辑判断；
  * 返回：把最后一个满足的结果，返回过来；
  * 返回：当遇见不满足情况，直接就把不满足结果返回；
  * 遇见：非Boolean值；转换为布尔值参与逻辑判断，返回最后那个是true判断的结果

#### 算术操作符

* 返回：就是数字类型计算的结果

```js
// +  -  *  /  % 
// ++ --
```

##### 字符串+

- **字符串+**：与字符串临近的类型，转为字符串；里面存在一个**隐式转化**；看不到的转化；
- 隐式转化：在字符串+情况下，数字隐转为字符串；
- 情况：
  - 字符串 + ；
  - +字符串;

##### 字符串 其他

- 字符串遇见 * / -；
- 隐式转化：字符串会转为数字，再次参加运算；

#### 比较操作符

- 语法：比较两个值的大小，**常规比较就是数字**
- 返回：**比较后的结果，对或错，Boolean值；标示状态成立与否；**

```js
// 语法：>  <  >=  <=
```

`==` 和 `===`区别：

- `==` 
  - **同类型：比较值是否一样；特别NaN==NaN  false**
  - **不同类型：转为数字类型，看值是否一样；**
- `===` 
  - **同类型：再看值；**
  - **不同类型：false**;

#### 逻辑操作符

* 语法：&&  ||  ！
* &&且：所有条件都要满足的情况下;

```js
true&&true  //true;
true&&false    //false;

1&&2   // 2;
```

* 特点：遇见有一个false，那么就直接返回false;

```js
// 用户在登录的时候要用户名和密码同时正确才能登录
var userName = prompt('请输入用户名');
var password = prompt('请输出密码');
console.log(userName === 'admin' && password === '123456');
// 只有 && 两边的 结果都是 true ，最终结果返回最后一个成立的结果；
```

* `||` 或：只要你有满足
  * 特点：只有有一个true，那么就直接返回是true的这个结果;

### continue和break

* continue：本次循环跳过，继续往后执行循环
* break：直接退出循环

### 三元表达式

* 表达式1 ? 表达式2 : 表达式3;
  * 如果表达式1成立，则把执行表达式2，要是不成立则执行表达式3

### 参数-arguments

* 本质是个对象，也可以循环遍历，可以获取所有的传入函数的实参
* 函数内部的变量

### 预解析

* 也叫变量提升，就是将声明的变量和函数提升到当前作用域的最顶端

### 对象添加属性

```js
  var obj = {};
1、点获取
  //语法 对象.方法名 = 函数(匿名函数)
  //函数什么时候才会执行？调用的时候才会执行；
  obj.say_name = function() {
    console.log(obj.name);
}
2、// 声明方式：键值对的方式声明；
  // 语法：对象["属性名"]  = 属性值；
  obj["name"] = "狗蛋";
  obj["age"] = 45;
```

### 对象-获取及遍历

```js
// key：泛指 代表 对象上的每对键值对的 键；
  for (var key in obj) {
    // console.log(key);

    // 获取方式：
    // 点方式：obj.key 为什么会输出 undefined；
    // 把obj.key 这个key 当做一个属性名；
    // console.log(obj.key);

    // ["属性名"]，只能通过键值对的方式获取值
    // console.log(obj[key]);
 	
    console.log(key, obj[key]);

  }
```

### 挑选数组里下标为偶数

filter的优势

- 直接出来一个数组

如果是for循环的话

- 需要声明一个新的空数组，用push进行塞入

**把看起来相似的东西放在一起来比较**

## splice和slice

#### slice截取/substring截取

slice可以设置负数，谁为负数，谁就和数组的长度相加得到该位置的数。

- 写法1：arr.slice(1,4)


- 截取，包左边不包右,也就是只到3；
- 不对原数组进行操作，返回的是新数组；
- 写法2：arr.slice(1);
  - 一直截取到倒数第二位
- 写法3 ：arr.slice();
  - 相当于给arr进行赋值

#### splice

```js
// 数组的splice方法用于从数组的指定位置移除、添加、替换元素

// 对原数组操作
// 作用：从索引3开始移除，总共移除1个元素 ，
// 返回 被移除数据的数组
arr.splice(3,1); 
console.log(arr);

// 添加数据
  // 下标3：代表第四个位置，
  // 第二个参数：删除0个；
  // 从下标3的位置，添加后面的数据（第三个和第三个参数）
  // var res = arr.splice(3, 0, "abc", "def");
  // 返回的是空数组；
  // console.log(arr, res);

// 修改，替换数据
  // 逻辑：删除的逻辑。
  // 把删除的位置的数据，替换为其他数据；
  // var res = arr.splice(3, 1, "abc");
  // console.log(arr, res);
```

### round

* 四舍五入

### 数组类型

* 类型为object

### 数组的复制

- 使用foreach遍历数组，再push给新数组
- 使用filter返回true
- slice（）截取，一直截取到最后，返回的是新数组
- concat() 进行拼接，返回的是新数组

```js
var new_arr = [];
arr.forEach(function(item,index,arr){
  new_arr.push(item)
});

var new_arr = arr.filter(function(item,index,arr){
  return item;
});

var new_arr = arr.concat();

var new_arr = arr.slice();
```



### Array-与字符串互转

```js
var arr = [1, 2, 3];
  console.log(arr);
  // 转为字符串
  // 不指定分隔符，默认用,  
  var str = arr.join("-");
  console.log(str);

```

### Array-查找元素

```js
 // 用于：判断这个数据在不在当前的数组；
 var arr = [1, 10, 20, 30];

  // 在数组中 返回下标
  // 不在：返回-1；
  // var index = arr.indexOf(10);
  // console.log(index);


  // 返回按照条件的第一个数据的下标（索引）
  var res = arr.findIndex(function(item) {
    // 判断的条件：条件这可以根据业务自己设置；
    return item > 50;
  });

  // 没有满足条件的时候，返回-1；
```

**拼接与截取不改变原来的数组，返回的是一个新的数组**

### es6新标签

```js
`${},${}`:字符串拼接

```

### 参数

```js
把需要换掉的部分配置为参数
如何去配置参数：
  // 根据你的业务需求，把一些你要抽象的数据，配置为参数。
  // 记得：在函数的()内，写上你配置的变量名；
  // 在声明函数的，内部的变量才算是声明了。
```

### 赋值

```js
//函数的调用：传入，赋值；不传入，函数内部默认给undefined
var obj = {};
obj[key] = value;
```

### return

* 作用1：返回值，后边要跟一个值
* 作用2：终止函数的执行

### 全局作用域和局部作用域

* 全局变量：在你声明的这个作用域内，任何地方都可以访问；
* 局部作用域：声明的函数内部的范围；外面访问不到局部作用域内的变量；

### 对象-添加属性

```js
// 语法 对象.方法名 = 函数(匿名函数)
  // 函数什么时候才会执行？调用的时候才会执行；
  obj.as_name = function() {
    console.log(obj.name);
  }

  // 对象.方法名();
  obj.as_name();
```

### 遍历数组

```js
// item是数组中的每个元素，index是item的索引,arr表示当前数组；
// 对本数组操作，没有返回值；
arr_1.forEach(function(item,index,arr){
  console.log(item,index);
});
```

### 查找元素

#### findIndex和filter

* filter 筛选出数组中满足条件的数组，**返回是一个新的数组；**
* findIndex 方法用于查找满足条件的第一个元素的索引，如果没有，则返回-1;若满足条件，返回第一个元素的的索引;

```js
var arr = [10, 20, 30];
var res1 = arr.findIndex(function (item) {
  return item >= 20;
});
// 返回 满足条件的第一个元素的的索引
console.log(res1); 
```

```js
var arr_1 = [1500,1800,2200,300,2600,800];
var res = arr_1.filter(function(item,index,arr){
  return item < 2000;
});
// fitler方法的的参数要求是一个函数，这个函数接收2个参数：item是数组中的每个元素，index是item对应的索引,arr代表当前的数组
```



### 清空数组

```js
var arr = [10, 10, 10];
  // console.log(arr, arr.length);
  arr.length = 0;

  console.log(arr);
```

### 匿名函数

* 自调用函数（自执行函数）：匿名函数的另外一种使用方法；很多时候，我们需要加载页面后，自动执行一个函数

```js
(function(){  
  console.log(10);  
})();
```

* 匿名函数：没有名字的函数，但是在js的语法中，是不允许匿名函数单独存在的，要配合其它语法使用：

```js
function (参数){
  函数体
}

var fn = function(a,b){
  return a + b;
}
```





