# WebAPI第二天

## 获取元素对象 选择器

* 要求：该选择器输入的值，主要为css选择器的写法，获取元素

```js
document.querySelector这个可以添加#或者.
```

```js
用法:document.querySelector(css选择器)
// 参数：多个css选择器，以逗号隔开，都是字符串
// 返回值：伪数组；for，但是上面有forEach方法
```

## 注册事件

```js
1、on本质相当于是把一个函数存储到 了 on 这个属性里面 ， 后面被重复赋值了，会覆盖；on的方式注册
2、addEventListener，可以多次注册事件，不会覆盖` 对象.addEventListener('事件类型', function() {})`
```

## 事件三个阶段

* 捕获 : 从根节点一层一层的向下找，一直到用户点击的那个DOM节点，
* 到达目标
* 冒泡 ：从DOM节点向上一层一层的找，一直到根节点
  * 冒泡执行：当向上找的时候，发现某个元素也注册了同类型的事件，也会执行对应的事件处理程序，**事件默认是在冒泡阶段执行**

捕获阶段

```js
// 对象.addEventListener('click', function() {
    console.log('我是你爷爷');
  }, true);
```

冒泡阶段

```js
// yeye.addEventListener('click', function() {
    console.log('我是你爷爷');
  }, false);
```

阻止冒泡

```js
`阻止冒泡： e.stopPropagation();`

// erzi.addEventListener('click',function(e){
  // 调用阻止事件冒泡的方法进行阻止
  // 事件对象 e 把该次点击这个过程看成一个对象
  e.stopPropagation();
  console.log('我是你儿子');
});
```



## 操作属性

```js
写法：
元素.setAttribute(属性名,属性值)
//作用：添加或者修改属性的值， 用于自定义属性

元素.removeAttribute(属性名)
//作用：删除某个属性

元素.getAttribute(属性名)
//作用：根据属性名获取属性值。
// 参数： 要获取的属性名,标准属性和自定义属性都可以。
```



## 案例—鼠标小飞人

### 注意事项

```js
1、//图片如果使用position: absolute，那下边用的是e.pageX/e.pageY（相对于整个页面）
//图片如果使用position: fixed，那下边用的是e.clientX/e.clientY（相对于可视窗口）
2、// 获取图片的位置，因为img使用了定位才可以改变行内的style的top值和left值。
3、img.style.top = `${y}px`，运用style控制行内样式，注意【`${y}px`】这个es6的写法，尤其是那个单位px；
```

## 案例—点击盒子移动

```js
//注意开关思想
```

## 开关思想—抽奖

```js
//元素对象.style.样式属性名 = ``来赋值；
```

## 事件委托

* 属性：innerHTML，可以获取标签内的HTML结构，也可以设置HTML结构；
* 作用：也可以添加子元素

```js
// ul.innerHTML += `<li>我是第${Math.random()}个li</li>`;
因为会把之前的覆盖掉，所以要 += 
```

* 弊端：每次新的时候，都要重新获取全部LI，重新每个都注册一次事件

### 使用e.target

```js
e为事件对象，target为e的属性
1、委托给父亲上
// ul.addEventListener('click',function(e){
    nodeName点击的这个DOM节点的标签名 ：大写
   if(e.target.nodeName === 'LI'){
   // 点击的就是li - 就执行代码
      console.log('li被点击了');
    }
 });
2、点击谁就是谁
```



