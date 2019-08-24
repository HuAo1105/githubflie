# WebAPI第二天

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



## 案例—鼠标小飞人

### 注意事项

```js
1、//图片如果使用position: absolute，那下边用的是e.pageX/e.pageY（相对于整个页面的左上角）
//图片如果使用position: fixed，那下边用的是e.clientX/e.clientY（相对于可视窗口）
2、// 获取图片的位置，因为img使用了定位才可以改变行内的style的top值和left值。
3、img.style.top = `${y}px`，运用style控制行内样式，注意【`${y}px`】这个es6的写法，尤其是那个单位px；
```

## 案例—点击盒子移动

```js
// 注意开关思想
```

## 开关思想—抽奖

```js
// 元素对象.style.样式属性名 = ``来赋值；
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

* 事件源(e.currentTarget)
  * 给谁注册了，谁就是那个源头

```js
 // 点击的哪个DOM节点，反给我的就是哪个DOM节点；
// 事件的目标对象，用户点击到谁上面了；用于事件委托；
 // console.log(e.target);

 // 返回 事件源
 // 给谁注册了，谁就是那个源头
 // console.log(e.currentTarget);
```



