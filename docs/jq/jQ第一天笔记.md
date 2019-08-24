## jquery的顶级对象

* $，又是一个jQuery的一个别称

## 入口函数

* $(function () {});
* $(document).ready(function(){
     ...  //  此处是页面DOM加载完成的入口
  });

## 区分DOM对象和jquery对象

* 用dom方法获取的节点就是dom对象
* 用$方法获取的节点就是jquery对象
* 属性和方法不能混用，各用各的
* 修改样式：$('div').css('属性', '值')

## DOM和jQuery之间的转换

* 因为JQ只是封装JS部分功能，有时候还需要用JS的方法去操作，所以我们要转换
* DOM ==> jQ对象
  * 用$把用DOM方法获取的节点直接塞进（）里
    * $(DOM对象)
* jQ对象==> DOM 
  * 通过索引    $('选择器'[index]);



## jq和js索引值的区别

* jq注册的事件，本身就有索引值$(’ul‘).index();


* js注册 的事件虽然是一个伪数组，但是本身没有索引值，需要手动添加lis[i].index = i ;
* jQuery得到当前元素索引号$(this).index();



## onmouseover和onmouseenter的区别

* onmouseover：支持冒泡
* onmouseenter：不支持冒泡

## 冒泡的补充

* 只要事件发生了，捕获和冒泡就发生，但是只能监听到一项

## **jQuery** 常用API

### jq选择器

* **$(“选择器”)   // 里面选择器直接写 CSS 选择器即可，但是要加引号** 

```js
$('#id')==》指定id元素

$('*')==》所有元素

$('.class')==》指定class元素

$('div')==》根据标签获取元素

$('div,p,li')==》获取多个

$('li.class')==>交集获取

$('ul>li')==>子代

$('ul li')==>后代
```

#### jq筛选方法!!!

>$('li').parent()   父级;   可以多次向上找父级
>
>$('ul').children('li')   子代    如果不加参数，获取所有的，如果添加指定的元素，按照指定的找
>
>$('ul').find('li')     后代
>
>$('li').siblings('')     兄弟【里边如果不写的话，指的是所有的同级的兄弟；如果写了的话，可以指某个】
>
>$('li'),nextAll();后面的
>
>$('li').prevAll();前面的
>
>判断是否有某个类名   $('div').hasclass('aaa')
>
>$('div').eq(index);指定的索引方法

```js
重点记住： parent()  children()  find()  siblings()  eq()
```

#### 小知识点

* 添加事件，show（显示）方法，hide（隐藏）方法，toggle（切换）方法
* this指的还是事件源

#### jq里排他思想

* 找到当前元素的其他的兄弟元素（显示或隐藏）

```js
$(this).css(“color”,”red”);

$(this).siblings(). css(“color”,””); 
```

#### 隐士迭代和链式编程

* 自动遍历函数
* 链式编程：从当前元素出发
  * $(this).css('color', 'red').sibling().css('color', ' ');  

#### 筛选选择器

>$('li:first')：第一个元素
>
>$('li:last')：最后一个元素
>
>$('li:eq(2)')==>索引为2【查找指定索引的元素】
>
>$('li:odd')==>索引为奇数
>
>$('li:even')==>索引为偶数
>
>注意：索引是从0开始的

### jQ样式操作

* 直接修改css选择器
* 操作类名

#### 操作css方法

```js
参数只写属性名，则是返回属性值【$(this).css(''color'');】

参数是属性名，属性值，逗号分隔，是设置一组样式，属性必须加引号，值如果是数字可以不用跟单位和引号【$(this).css(''color'', ''red'');】

参数可以是对象形式，方便设置多组样式。属性名和属性值用冒号隔开， 属性可以不用加引号，
【$(this).css({ "color":"white","font-size":"20px"});】

eg: $('li').css('background','blue');
```

#### 设置类样式方法

```js
添加类【$('div').addClass('current')】
移除类【$('div).removeClass('current')】
切换类【$('div').toggleClass('current')】

原生JS中className会覆盖元素原来的类名

jQ里面操作只是对指定的类进行操作，不影响原来的类名
```

### jQ效果

显示隐藏效果

```js
show 显示
hide 隐藏
toggle 切换

show([speed,[easing],[fn]])
hide([speed,[easing],[fn]])
toggle([speed,[easing],[fn]])

(1)、参数都可以省略，无动画直接显示
(2)、speed：三种速度slow、normal、fast，或者直接写动画时长的毫秒数
(3)、easing：默认是swing，可以设置成linear
(4)、fn ：回调函数，在动画完成时执行的函数，每个元素执行一次

$('#btn2').click(function () {
			$('div').hide(1000,'linear',function () {
		console.log('hideOK');
	});
});
```

#### 滑动效果

````js
slideDown   向下划
slideUp     向上划
slideToggle 切换

slideDown([speed,[easing],[fn]])
slideUp([speed,[easing],[fn]])
slideToggle([speed,[easing],[fn]]
````

#### 切换事件

* hover([over], out)

```js
（1）over:鼠标移到元素上要触发的函数（相当于mouseenter）
mouseenter==mouseover
（2）out:鼠标移出元素要触发的函数（相当于mouseleave）
mouseleave==mouseout
（3）如果只写一个函数，则鼠标经过和离开都会触发它
```

#### 动画队列及停止排队方法

```js
动画或者效果一旦触发就会执行，如果多次触发，就造成多个动画或者效果排队执行。

停止排队:stop()

(1）stop() 方法用于停止动画或效果。
// (2)  注意： stop() 写到动画或者效果的前面， 相当于停止结束上一次的动画
```

#### 淡入淡出效果

```js
fadeIn      淡入
fadeOut     淡出
fadeToggle  切换
fadeTO      淡入淡出的程度   【注意fadeTo必须写两个参数，speed和opacity】
fadeTo(时间，透明度)
```

#### 自定义属性animate

* 动画不可以改背景颜色，一般添加带数字的属性

### 误区

```js
this指得是当前事件源

如果this在jq里只写this的话，获取的是当前整个标签，包括html结构

$(this)这样写的话，获取当前注册 的事件
```













