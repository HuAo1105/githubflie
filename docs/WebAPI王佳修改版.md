# WebAPI第一天



# WebAPI

- API - application   programing   interface 翻译过来叫 `应用编程接口` 
- javascript组成
  - ECAMAScript：js的语法规范；js基础6天所学 -，简称es；
  - **DOM - document object model - 文档对象模型 -  把整个页面（document）看成一个对象**；其实是树形模型，树形结构里面的每个交叉点（标签），被称为 `节点`  ，也叫**DOM节点**；我们现在认知的节点包括**： 标签本身、标签上的属性（src、id、class、style等）、标签内文本；
  - BOM - browser object model - **浏览器对象模型 - 把浏览器看成一个对象**；





# DOM

# 获取元素对象的方法  

## Byld

* 作用：根据ID获取元素对象

- 参数：要获取的元素对象或者（DOM节点）的ID的**字符串**；
- 返回值：返回当前节点对象，也是我们在页面上看见节点，若是没有找到这个标签，返回为null ，null对象类型，代表空；

```js
var closeBtn = document.getElementById('close');

// 获取body，因为body比较特别；永远只有一个；
document.body
```

## ByTagName

作用：根据标签名获取元素

参数：标签名--必须是字符串

返回值：一个伪数组，可以用for遍历 - 里面包含有所有满足条件的元素

```js
document.getElementsByTagName("tagname");
```



 

## ByClassName

作用：根据元素类名获取元素

参数：类名--必须是字符串

返回值：一个伪数组，可以用for遍历 - 里面包含有所有满足条件的元素 

```js
document.getElementsByClassName("classname");
```



##  querySelector(css选择器)

作用：根据指定的选择器获取从上到下的第一个元素，获取不到返回个null对象,只返回一个；

参数：css写法写的css选择器----必须是字符串

返回值：根据指定的选择器获取从上到下的第一个元素

``` js
document.querySelector(css选择器);
var box=document.querySelector("#box")
```



##  querySelectorAll(css选择器1,css选择器2...)

作用：（1）根据选择器获取所有满足条件的元素，这个使用的比较多；

​             （2）一般用于类名和标签名的DOM节点获取

参数：多个css选择器，以逗号隔开，都是字符串

 返回值：伪数组；for，但是有forEach方法

```js
document.querySelectorAll(css选择器1,css选择器2...);
```



# 注册事件  

* 步骤：
  * 1.获取DOM节点
  * 2.注册事件：
    * 注册给谁？元素对象（DOM节点）；
    * 注册什么事件类型？
  * 3.事件响应之后要怎么办？函数体内部的代码；匿名函数 事件处理程序(函数)

## click

* 注册给谁：DOM节点

* 事件类型：用户点击

```js
 // click 事件类型：用户通过什么行为,去触发一件事
// 匿名函数 事件处理程序(函数)：做了这个行为之后，要做什么事情；
btn.onclick = function(){
  console.log('被点击了');
}
```

## focus----blur

- focus：聚焦；blur：模糊；
- 注册给谁？有光标的盒子input textarea;
- 事件类型：
  - 有光标时：获得焦点focus；
  - 无光标时：失去焦点 blur

 ```js
ipt.onfocus = function(){
  // 当你想要让鼠标光标在输入框里面的时候要做什么事，就使用这个事件即可
}

ipt.onblur =  function(){
  //当你希望处理鼠标光标失去的时候所做的事情，就在这里做
}
 ```

```js 
// 1 获取元素
var search = document.getElementById('search');
var list = document.getElementById('list');
// 2 注册获得焦点的事件
search.onfocus = function(){
  // 把搜索历史显示 - 通过修改display属性 - 元素.style.display = 'block';
  list.style.display = 'block';
}

// 2 注册失去焦点事件
search.onblur = function(){
  // 把搜索历史隐藏 - 修改display为none
  list.style.display = 'none';
}
```

##  mousedown----mousemove----mouseup

注册给谁？DOM节点

事件类型：mousedown：当鼠标的按键被点下的时候触发
                  mousemove：鼠标在某个元素身上移动的时候触发
                  mouseup ：当鼠标的按键被松开的时候触发

## on事件名 

- 无法多次注册；后面被重复赋值了，会覆盖会把你的覆盖了。

  ```js
  var btn = document.querySelector('#btn');
  btn.onclick=function(){}
  ```

## addEventListener

作用：添加事件监听，可以多次注册事件，不会覆盖；

参数： 两个参数：事件类型 - 字符串； 事件处理程序 - function 

 返回值：undefined

```js
var btn = document.querySelector('#btn');
btn.addEventListener('click', function() {
    console.log(123);
})
btn.addEventListener('click', function() {
    console.log(456);
})
//两种结果都会被打印
```

# 事件三个阶段

## 冒泡

- 事件发生（事件点击）的时候，必然存在这三个传播的阶段：**捕获、到达目标、冒泡；**

  由外到内的过程（从html到点击事件）-----------捕获

  到达目标-------------目标

  由内到外的过程（从点击事件到html）------------冒泡

* 冒泡执行：**事件默认是在冒泡阶段执行：和目标DOM节点注册同样的事件，也会执行；**

## 阻止冒泡

过程：

* 需要先得到事件对象，给处理程序添加一个形参e就行

- 你希望在哪里阻止（在冒泡阶段执行的后面的事件，不再执行），就在哪个事件处理程序里面调用即可e.stopPropagation();在函数里面的前后位置无所谓；
- Propagation：传播；

```javascript
// 要阻止冒泡，需要先得到事件对象，给处理程序添加一个形参就行
erzi.addEventListener('click',function(e){
  // 调用阻止事件冒泡的方法进行阻止
  // 事件对象 e 把该次点击这个过程看成一个对象
    //在冒泡阶段执行的后面的事件，不再执行
  e.stopPropagation();
  console.log('我是你儿子');
});
```

 

# 事件对象

- 事件对象： 一个集合体，描述点击的这个行为（点击位置，点击了谁，注册给谁这些）,就是鼠标

```js
// 获取事件对象
事件源.on+事件类型 = function(事件对象e){   }

事件源.addEventListener(事件类型,function(事件对象e){});
```

* 四个属性：

```js
鼠标位置

// 可视区域坐标系 - 以浏览器的可视区域的左上角为原点的
// 可视区域：就是元素用来显示内容的区域
事件对象.clientX
事件对象.clientY

// 页面坐标系  -  以body的左上角作为原点
事件对象.pageX
事件对象.pageY



点击了谁
// 事件的目标对象，用户点击到谁上面了,就返回谁DOM节点；
事件对象.target


注册给了谁
// 事件的绑定对象，就是是绑定在哪个DOM节点上 和 this一样，说的事件源
 事件对象.currentTarget==this -----> true
```

- 方法：

```js
// 阻止冒泡
事件对象.stopPropagation();

// 阻止默认行为；
事件对象.preventDefault();


// 页面右键事件 查看右键菜单
document.oncontextmenu = function(e){
  e.preventDefault();
}

// 阻止a标签转跳
// 1 把a标签的href属性设置为 javascript:void(0);
// 2 在a标签的点击事件里面，return false;
// 3 使用事件对象.preventDefault();
dom_a.addEventListener('click', function(e) {
    e.preventDefault();
});

```

# 事件委托

### 引入

- 属性：innerHTML，可以获取标签内的HTML结构，也也可以设置HTML结构；
- 设置可以把以前的数据覆盖

```
  var ul = document.querySelector('ul');
  var btn = document.getElementById('btn');
  btn.onclick = function () {
    // 给ul添加新的元素
    var old = ul.innerHTML;
    old += '<li>新的li</li>'
    ul.innerHTML = old;
  }
```

- 需求：给li标签注册点击事件，新增的li标签也要有点击事件；

```js
  var lis = document.querySelectorAll('ul > li');
  // console.log(lis);
  // 注册事件
  for (var i = 0; i < lis.length; i++) {
    lis[i].onclick = function () {
      console.log(123);
    }
  }

  var ul = document.querySelector('ul');
  var btn = document.getElementById('btn');
  btn.onclick = function () {
    // 给ul添加新的元素
    var old = ul.innerHTML;
    old += '<li>新的li</li>'
    ul.innerHTML = old;
  }

```

### 实现

- 什么是事件委托？
  - 把事件注册在父级的元素身上，
  - 利用事件冒泡执行，当事件传播到已经注册了事件的父级元素身上，
  - 判断  触发事件的DOM  （e.target）节点是否是指定的元素，e.target.nodeName=="LI"
    - 如果是，就执行逻辑，
    - 否则什么都不管；
- **什么时候用？**
- **当我们需要给动态创建（不是一开始写死的，是后期可能会变的元素）的元素实现注册事件的效果的时候；**

```js
  // 利用ul的点击事件，模拟实现给li注册事件的过程
  ul.addEventListener('click',function(e){
    // 判断被点击的是不是子元素li
    // 只要判断 e.target 是否是我的子元素即可
    // 判断e.target 是否是 li 元素, 节点都有一个属性 ： nodeName 里面就是 大写的标签名
    // 只需要判断 nodeName 是不是LI 即可
    if(e.target.nodeName === 'li'){
      // 点击的就是li - 就执行代码
      console.log('li被点击了');
    }
      
      
    // 在事件对象中，还有一个属性target，这个属性指向事件目标
    // 注意，this目前拥有指向 注册事件的元素；e.currentTarget指向绑定事件的元素的对象，事件源；
    console.log(e.target,e.currentTarget==this);
    
  });
```



# 获取元素对象 位置

- style属性：只能获取行内样式设置的位置信息

  获取元素到参考父亲上边和左边的距离





* 元素的offsetParent:找到一个有定位的父亲元素，如果亲生父亲没有定位，会一直往上找，直到找打有定位的父亲，或者body；
* 元素.offsetLeft

​       作用：得到的是某个元素距离他的offsetParent元素的水平距离；

​                  元素.offsetLeft = marginLeft + left

​       返回值：元素对象的位置：获取到的是数值；

- 元素.offsetTop 

​         作用：得到的是某个元素距离他的offsetParent元素的垂直距离；

​                  元素.offsetTop = marginTop + top

​       返回值：元素对象的位置：获取到的是数值； 



 

# 事件解绑

- 案例：抽奖只能点击一次
  - **开关思想**；一般如果遇见：一开始没有，后边有；一开始有，后边没有的，状态的变化，就要用到开关思想

     一般来说，会给变量设一个true或false

  - **事件解绑******(事件注销)**；
- 开关思想：

```js
  // 一开始，没有点过
  var isClick = false;
  // 获取按钮，注册点击事件
  var begin = document.querySelector('.begin');
  var zhizhen = document.querySelector('.zhizhen');

  var angle = 0
  begin.onclick = function() {
    // false证明没有点击过，就可以点
    if (isClick === false) {
      // 点下之后，把开关关掉
      isClick = true;
      // console.log('点击过了');
      angle += Math.random() * 360 * 6;
      // 4 修改指针的transform  transform: rotate(10deg);
      zhizhen.style.transform = 'rotate(' + angle + 'deg)';

    }
  }
```

- 事件解绑：事件无效；
  * 作用：曾经注册了的事件，在触发之后，无法执行对应的事件处理程序了；

  - 过程：事件触发的时候，把事件解绑。那么下次你再次点击的时候，就无效了，解绑的前后位置无所谓。

  注册事件为click:    DOM节点.onclick=null;

  注册事件为addEventListener   函数需要函数名:    DOM节点.removeEventListener('注册事件',函数名);

```javascript
var btn = document.getElementById('btn');
btn.onclick = function(){
    //解绑，位置前后无所谓
  btn.onclick = null;
  console.log('谢谢惠顾');
}

var btn = document.getElementById('btn');
btn.addEventListener('click',function fn(){
  // 解绑 当前的函数
  btn.removeEventListener('click',fn);
  console.log('抽奖了');
})
```







# 属性

## 标准属性

* 标签原有的属性

* **操作属性？**我们可以通过拿到的DOM节点，对DOM节点的上的这些属性直接进行操作（修改）

  

### 样式属性：通过style或className或classList操作元素样式

#### style

- 作用：style属性以对象的方式管理里面的多个**键值对**，元素对象.style可以看作是对象

- 获取：通过  `元素对象.style.样式属性名`， 只能获取行内样式；
- 设置：通过 `元素对象.style.样式属性名=“  ”；直接赋值
- 如果样式属性名是多个单词的，需要把样式属性的`-` 去掉，修改为驼峰命名；

```js
// 获取：只能获取行内样式；
div.style.backgroundColor
// 设置
div.style.backgroundColor = ’#fff‘;
```

- 连起来：点击盒子，变背景色；

```js
var closeBtn = document.getElementById('close');
closeBtn.onclick = function(){
  closeBtn.style.backgroundColor = ’red‘;
}
```





#### className：DOM节点上的class**属性
- 作用：可以添加或修改我们已经写好的类名；更快的跟换样式；
- 需要用className才能正常输出元素的class属性
- 修改样式：在原来的基础上进行添加类名box.className += '新的类名';

```js
console.log(元素.class); // 输出undefined
console.log(元素.className); // 正常输出元素的class属性

// 如果要修改类样式，只需要把className修改一下就行了；
// 但是会直接覆盖
box.className = '新的类名';

// 解决：在原来的基础上进行添加类名
box.className += '新的类名';
```



#### classList：管理着所有类名的属性对象

* 作用：管理着所有类名，来改变样式**比较好的方式解决上面的覆盖问题；**

- 操作什么：类名；
- add：给元素对象添加一个或者多个类名，不会影响原来的类名；

```javascript
// 参数：多个类名，之间用逗号隔开
box.classList.add(类名1,类名2...)；
```

- remove： 给元素删除一个或者多个类名，

```javascript
// 参数：多个类名，可以是多个，多个之间用逗号隔开
box.classList.remove(类名1,类名2...)
```

- toggle：切换类名：有类名就删除，没有就加上；

```javascript
// 参数： 要切换的类名
box.classList.toggle(类名)
```

- 案例：优化搜索区显示隐藏

```js
// 注册获得焦点事件
search.onfocus = function(){
  // 给搜索历史添加一个类名 （show）
  list.classList.add('show');
}

// 注册焦点的失去事件
search.onblur = function(){
  // 把show这个类名移除
  list.classList.remove('show');
}
```



### value src原有属性
 * 获取和设置DOM节点的value值

```js
var text = btn.value;

btn.value = "新的字符串";
```

一个按钮 开关灯

- 业务：
  - 背景为开灯状态，按钮显示值为关灯，点击后关灯；
  - 背景为关灯状态，按钮显示值为开灯，点击后开灯；
- 步骤：
  - **获取元素**：按钮，body
  - **注册对应的事件**:click
  - **点击之后**：找到当前的显示的值是什么，进行不同的条件的判断；

```js
btn.onclick = function(){
  // 判断当前的文字是否为关灯
  var text = btn.value;
  if(text === '关灯'){
    // 把灯关掉
    document.body.style.backgroundColor = '#000';
    // 把文字变成开灯
    btn.value = '开灯';
  }
  // 开灯状态，我要关灯，设置为关灯；
  else {
    // 文字是开灯，把灯打开
    document.body.style.backgroundColor = '#fff';
    //把文字修改为关灯
    btn.value = '关灯';
  }
}
```

案例：点击按钮切换图

- 业务：点击多个按钮，切换不同的图片进行显示
- 步骤：
  - 获取元素：按钮、图片；
  - 注册事件：点击
  - 事件函数：获取图片上的自定义数据，设置给图片属性；

```js
    var img = document.getElementById('img');
	// 伪数组：只能使用for循环；
    var btns = document.getElementsByTagName('input');
	
	// for循环；
    for (var i = 0; i < btns.length; i++) {
      // 给每个元素绑定事件，
      // 什么时候执行？点击的时候执行；
      btns[i].onclick = function() {
        
        // 这个地方，为什么不能用 btns[i].dataset.src
        // 点击的时候，循环已经完成，所以后打印 btns[i] 为undefind;
        console.log(this, btns[i]);
        // 通过this,找到注册事件的事件源 DOM节点，获取自定义属性；
        img.src = this.dataset.src;
      }
        
    }
```




### 开关属性：checked，selected,disabled
- 开关属性： checked/selected/disabled ，这种只有两种状态的属性；
- 赋值：两个状态的值，布尔类型；

```js
var ck = document.getElementById('ck');

ck.checked = true;
ck.checked = false;
```

设置为禁用

 ``` js
btn.disabled=true
 ```




## 自定义属性
- **自定义属性**： 自己胡乱命名的，**没有什么功能，就是自己需要**；
- 命名: 在标签上已自定义属性 以 data-属性名
- 获取：以 data- 开头的自定义属性，都存储在了 元素.dataset 这个对象里面ipt.dataset.src
- 事件执行函数：内部如何获取到DOM节点的自定义属性；可以通过标签，也可以通过this;

```js
// 命名: 在标签上已自定义属性 以 data-属性名
<input type="button" value="美女1" data-src="./images/01.jpg" />
    
// 获取：以 data- 开头的自定义属性，都存储在了 元素.dataset 这个对象里面
ipt.dataset.src
```

- 事件执行函数：内部如何获取到DOM节点的自定义属性；可以通过标签，也可以通过this;

```js
btn_2.onclick = function(){
  // 修改图片的src属性
  img.src= btn_2.dataset.src;
  // this，只当前事件执行的事件源本身；
  img.src= this.dataset.src;
}
```

## Attribute系列方法推荐操作自定义属性!!!

* 元素.getAttribute(属性名)

  作用： 根据属性名获取属性值

​       参数： 要获取的属性名,标准属性和自定义属性都可以。

​                    而且自定义属性不再限制于 data-属性 的格式要求

​       返回值： 字符串

 ```js
btn.getAttribute("属性名")；
 ```

* 元素.setAttribute(属性名,属性值)

作用： 添加或者修改属性的值

 参数：两个参数，一个属性名，一个属性值，都是字符串；

```js
btn.setAttribute("属性名","属性值")；
```

* 元素.removeAttribute(属性名)

​       作用：删除某个属性  

​       参数：要删除的属性名

```js
btn.removeAttribute("属性名")；
```





# 案例：全选盒子

### 业务

- 点全选 选择 ，下面所有盒子都选择；
- 点全选 取消，下面所有盒子都取消
- 下面盒子点选择，全部都选择后，全选按钮会自动选择；
- 下面盒子点选择，只要有一个没有选择，全选按钮就不会选择；

### 功能：全选与取消

- 获取元素：全选盒子、下面的子盒子
- 注册事件：全选盒子click
- 点击之后：点全选 选择 ，
  - 拿到全选后的状态；
  - 循环遍历给子元素 赋值状态；

```js
  var ckAll = document.getElementById('checkAll');
  // 伪数组
  var cks = document.getElementsByClassName('ck');

  // 2 给全选注册点击事件
  ckAll.onclick = function() {
    // 3 获取当前是否勾选
    var status = ckAll.checked;

    for (var i = 0; i < cks.length; i++) {
      cks[i].checked = status;
    }
  }
```

### 功能：子选项全选，父选项自动变为选择

- 获取元素：全选盒子、下面的子盒子
- 注册事件：子盒子注册click（循环）
- 点击之后：
  - 假设现在是子选项全部选中，标示key=true;
  - 循环遍历，看子选项有没有 无选中的盒子
    - 有：key=false;终止循环
    - 无：key仍然还是true；
  - 判断key
    - true：全部选中，父选项 变为选中；
    - false：有没有选中的子选项，父选项 不选中；

```js
  for (var i = 0; i < cks.length; i++) {
    cks[i].onclick = function() {
      // 使用反证法实现判断是否全选
      // 3.1 假设全都选中了
      var flag = true;
      // 3.2 循环的去找反例，只要有一个没勾选，就推翻假设
      for (var j = 0; j < cks.length; j++) {
        if (cks[j].checked != true) {
          // 至少有一个没有勾选，推翻假设
          flag = false;
          break;
        }
      }
      // 3.3 再次判断假设是否成立
      if (flag) {
        // 如果是true，证明全都勾选，设置全选是选中的
        ckAll.checked = true;
      } else {
        // 证明没有全都勾选，设置全选是取消选中的
        ckAll.checked = false;
      }
    }
  }
```

# 案例：鼠标拖到一个盒子进行移动；



- 实现

  - 获取元素：盒子
  - 注册事件：onmousedown、 onmousemove、onmouseup
  - 事件之后：
    - onmousedown：
      - 记录：
        - 鼠标在盒子内部的位置；
          - 为什么要记录？因为鼠标在盒子内部的位置一直没变；
          - 记录什么？鼠标点击的位置
        - 鼠标键已经点击；
    - onmousemove：
      - 判断：鼠标键是否已经落下；
        - 没有落下：无操作
        - 落下：**计算盒子应该出现的位置 = 用新的鼠标位置 - 记录在内的一开始的位置；**
    - onmouseup：移动结束
      - 记录：鼠标键已经弹起；

  开关

```js
  var p_dom = document.querySelector('.p');
  
  var x_start = 0;
  var y_start = 0;

  var move_key = false;
  p_dom.onmousedown = function (e) {
    // 
    move_key = true;
    
    x_start = e.pageX - p_dom.offsetLeft;
    y_start = e.pageY - p_dom.offsetTop;
  }

  var x_yidong = 0;
  var y_yidong = 0;
  document.onmousemove = function (e) { 
    // console.log(1);
    
    if (move_key) {
      x_yidong = e.pageX - x_start;
      y_yidong = e.pageY - y_start;

      p_dom.style.top = y_yidong  + 'px';
      p_dom.style.left = x_yidong  + 'px';
    }
    
  }

  p_dom.onmouseup = function (e) {
    // 
    move_key = false;
  }
```



