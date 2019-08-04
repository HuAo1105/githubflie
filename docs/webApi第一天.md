# webApi第一天

**注意用哪个事件类型（lick、focus、blur），完了谁会显示效果**

1、Math.random()   这个是已经帮我们封装好的对象的属性和方法。

2、**DOM - document object model - 文档对象模型 -  把整个页面看成一个对象**；

* js组成：
  * ES：前六天js基础（尤其是数组的方法）

### 获取元素对象

* ：DoM节点
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



4、null为对象类型

### 标准属性-style

* 控制行内属性，获取行内样式，设置了就获取，不设置就获取空。

```js
// 获取：只能获取行内样式；
div.style.backgroundColor
```



* 为对象类型

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

### 事件类型

* lick
* focus
* blur

## 类样式

### className和classList

* 可以添加或修改我们已经写好的类名；更快的跟换样式；


* className：会覆盖掉原来的类名
  * 解决：box.className += ' 新的类名';**新的类名前边要加空格**
* classList：

```
用法：
classList.add("") 添加
classList.remove("")移除
classList.toggle("")切换类名
```

## 获取元素对象

### TagName和 ByClassName

* 循环时不能用foreach，他俩没有这个用法。


* TagName：获取标签名

```js
//参数： tagname - 标签名 - 必须是字符串
// 返回值： 一个伪数组 - 里面包含有所有满足条件的元素
// 伪数组：可以遍历；
```

* ByClassName：获取类名

```js
// 参数： classname - 类名 - 必须是字符串
// 返回值： 一个伪数组 - 里面包含有所有满足条件的元素
// 伪数组：可以遍历；
```

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

## 标准属性

* 开关属性： checked/selected/disabled ，这种只有两种状态的属性
* 赋值：两个状态的值，布尔类型；
* disabled 禁用

```js
用法：btn.disabled = true;
```



## 易错点

```js
//if条件里为双等于号 == 
if (info == "关灯") {
            document.body.style.backgroundColor = "yellow";
            dom_btn.value = "开灯";
        }
        else {
            document.body.style.backgroundColor = "red";
            dom_btn.value = "关灯";
        }
```





