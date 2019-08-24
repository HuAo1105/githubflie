# webApi第一天

* js组成：ECAMAScript，DOM，BOM
* 学习属性和方法

**注意用哪个事件类型（lick、focus、blur），谁会显示效果**

1、Math.random()   这个是已经帮我们封装好的对象的属性和方法。

2、**DOM - document object model - 文档对象模型 -  把整个页面看成一个对象**；

* js组成：
  * ES：前六天js基础（尤其是数组的方法）

### 获取元素对象

* DoM节点
* 通过id去获取节点

```js
document.getElementById('close');
括号里一定加引号，要不会被当成变量
```

3、点击是一个事件，要**注册在DOM节点**上，形成交流互动；点击之后触发匿名函数的函数体,作为一个响应。

```js
注册：
btn.onclick = function(){
  console.log('被点击了');
}
用户点击的时候才会执行这个函数。
```

### 获取元素对象

* TagName和 ByClassName
  * 循环时不能用foreach，他俩没有这个用法。
* TagName：获取标签名
* 伪数组不能用真正数组内置的方法（push、pop、sort）

```js
//参数： tagname - 标签名 - 必须是字符串
// 返回值： 一个伪数组 - 里面包含有所有满足条件的元素
// 伪数组：可以遍历；
document.getElementsByTagName('标签名')
```

* ByClassName：获取类名

```js
// 参数： classname - 类名 - 必须是字符串
// 返回值： 一个伪数组 - 里面包含有所有满足条件的元素
// 伪数组：可以遍历；
document.getElementsByClassName('类名')

// 这时应该想起：document.querySelectorAll('类名')
```

### 获取元素对象  选择器！！！

```js
// document.querySelector(css选择器);

// document.querySelectorAll(css选择器1,css选择器2...);
// 返回值：伪数组；for，但是这个伪数组上面有forEach方法
```

### 插件-获取对象元素

* var arr = $('css选择器')

### 获取元素对象位置

* 元素.offsetleft = marginleft + left 
* 元素.offsettop = margintop + top

```
offsetleft / offsettop 寻找父元素有无定位，若没有的话，就一直向上找，一直到body
```

### 获取实际宽高

* 元素.offsetHeight 获得元素的实际高度
* 元素.offsetWidth   获得元素的实际宽度

### 可视区域的宽度和高度

* clientWidth
* clientHeight

### 注册事件 

```js
// 对象.addEventListener('事件类型', function() {
    console.log(123);
})
	1、on本质相当于是把一个函数存储到 了 on 这个属性里面 ， 后面被重复赋值了，会覆盖；on的方式注册
	2、addEventListener，可以多次注册事件，不会覆盖


// btn.onclick = function(){
  console.log('被点击了');
}

// btn.on('swipeLeft', function(){
  
})
```



4、null为对象类型



### 标准属性

* style
  * 控制行内属性，获取行内样式，设置了就获取，不设置就获取空。
  * 为对象类型

```js
// 获取：只能获取行内样式；
div.style.backgroundColor

// 设置
div.style.backgroundColor = ’#fff‘;
```

* 开关属性： checked/selected/disabled ，这种只有两种状态的属性
* 赋值：两个状态的值，布尔类型；
* disabled 禁用

```
用法：btn.disabled = true;
```



### 三点

* 1、获取DOM节点

```js
var open = document.getElementById('open(id)');
```

* 2、注册事件

```js
open.onclick = function(){
    // 修改背景颜色
    document.body.style.backgroundColor = '#000';
};
```

### value

```js
使用txt.value来获取文本域的内容
```

### 事件类型

* click                       点击
* focus                   有光标时：获得焦点 
* blur                     无光标时：失去焦点
  * focus 、blur 用在input和textarea
* mouseover        鼠标进入
* mouseout          鼠标离开
* mouseenter        鼠标进入
* mouseleave        鼠标离开
  * mouseenter和mouseleave不会冒泡
* mousedown      鼠标向下点击
* mouseup           鼠标向上抬起
* onkeydown        按键按下
* onkeyup             按键弹起

### 用键盘实现确认发布

```js
// 按下ctrl和回车键发布

text.onkeydown = function(e) {
    if (e.ctrlKey && e.keyCode === 13) {
    }
}
```

## 类样式

### className和classList

> className 直接 += 赋值
>
> classLIst是通过一些方法来操控

* 可以添加或修改我们已经写好的类名；更快的跟换样式；
* classList：DOM元素对象的一个**属性对象**；管理着所有类名。


* className：会覆盖掉原来的类名
  * 解决：box.className += ' 新的类名';**新的类名前边要加空格**
  * 加上新的类名，可以在上边直接调用
* classList：

```
用法：
classList.add("类名1,类名2...") 添加
classList.remove("类名1,类名2...")移除
classList.toggle("类名")切换类名。本身如果有的话，就移除；如果没有，就添加上
```

## 排他思想

* 例如轮播图，我需要下边的数字和图片形成一致，首先要给当前的li添加上类名（使用classList.add），再利用排他思想（使用循环）把类名给去除掉（使用classList.remove）;

## 自定义属性

* 初始化定义:比如为**data-**开头的自定义属性，都存在了dataset这个对象里边。
* 如何获取

```js
例如:
img.src= btn_2.dataset.src;

// this，只当前事件执行的事件源本身，例如当点击第一张图片时；
img.src= this.dataset.src;
通过获取this图片路径赋给img.src;
```



* 自定义属性的用法
  * 解除定义时只能用date-开头的限制

```js
写法：
元素.setAttribute(属性名,属性值)
// 作用：添加或者修改属性的值， 用于自定义属性

元素.removeAttribute(属性名)
// 作用：删除某个属性

元素.getAttribute(属性名)
// 作用：根据属性名获取属性值。
// 参数： 要获取的属性名,标准属性和自定义属性都可以。
```



## 显示与隐藏

* list.style.display = 'none';    隐藏
* list.style.display = 'block';   显示

## 类名互换

* 先将后边的或者前边的删除掉，再插入到前边去

## 易错点

```js
// if条件里为双等于号 == 
if (info == "关灯") {
            document.body.style.backgroundColor = "yellow";
            dom_btn.value = "开灯";
        }
        else {
            document.body.style.backgroundColor = "red";
            dom_btn.value = "关灯";
        }
```

## 什么是事件对象

* 就是e（event）

## 移动端事件

- 向左划：swipeLeft
- 向右划：swipeRight
- 点击：tap
- touchstart - 会在手指触摸到屏幕的时候触发
- touchmove - 会在手指触摸到屏幕，移动的过程中触发
- touchend - 会在手指离开屏幕的瞬间触发
- 用一个手指触摸屏幕内的元素：
  - **刚触摸时touchstart**：touches、targetTouches、changedTouches，有一个值；都是同一个值；
  - **在元素上触摸移动时touchmove**：touches、targetTouches、changedTouches，有一个值；都是同一个值；
  - 离开屏幕：touches、targetTouches没有值；changedTouches有最后离开屏幕的值；


## 取消a标签默认行为

> 方式1：使用return false;
>
> ```js
> <a href="https://www.baidu.com" id="link">点击</a>
>
> <script>
> var link = document.querySelector('#link');
>
>     link.onclick = function() {
>         alert('nihao');
>         return false;
>     }
> </script>
> ```
>
> 方式2 ：设置a标签href属性值为：jasascript：
>
> ```js
> // 给a标签的href值设置javascript：，表示将来点击a时，会阻止默认跳转行为，并且仅仅会执行js代码
> <a href = "javascript:">点击</a>
>
> 扩展：通过a可以打开打电话应用
> <a href = "tel:">打电话</a>
> 扩展：通过a可以打开电子邮箱应用
> <a href = "mailto:">打开邮箱</a>
> ```
>
> 






