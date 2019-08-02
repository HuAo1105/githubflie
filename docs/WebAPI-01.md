# WebAPI第一天



# WebAPI

- API - application   programing   interface 翻译过来叫 `应用编程接口` 
- javascript组成
  - ECAMAScript：js的语法规范；js基础6天所学 -，简称es；
  - **DOM - document object model - 文档对象模型 -  把整个页面（document）看成一个对象**；其实是树形模型，树形结构里面的每个交叉点（标签），被称为 `节点`  ，也叫**DOM节点**；我们现在认知的节点包括**： 标签本身、标签上的属性（src、id、class、style等）、标签内文本；
  - BOM - browser object model - **浏览器对象模型 - 把浏览器看成一个对象**；
- WebAPI阶段：学习DOM和BOM的属性和方法，并使用它们实现页面上的效果；





# DOM

# 获取元素对象的方法 ById ----ByTagName--ByClassName  

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
document.getElementsByTagName(tagname);
```



 

## ByClassName

作用：根据元素类名获取元素

参数：类名--必须是字符串

返回值：一个伪数组，可以用for遍历 - 里面包含有所有满足条件的元素 

```js
document.getElementsByClassName(classname)
```





# 注册事件 click---focus---blur

* 步骤：
  * 1.获取DOM节点
  * 2.注册事件：
    * 注册给谁？元素对象（DOM节点）；
    * 注册什么事件类型？
  * 3.事件响应之后要怎么办？函数体内部的代码；匿名函数 事件处理程序(函数)

## click

* 事件类型：用户点击
* 注册给谁：DOM节点

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

# 属性

## 标准属性

* 标签原有的属性

* **操作属性？**我们可以通过拿到的DOM节点，对DOM节点的上的这些属性直接进行操作（修改）


### 样式属性：通过style或className操作元素样式

#### style

- **style属性：**

  - 作用：style属性里面的内容其实是多个**键值对**，js帮我们把它们以对象的方式管理起来；

    元素对象.style可以看作是对象

  - 获取：只需要  `元素对象.style.样式属性名` ；

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

## 案例

### 两个按钮 开关灯

- 业务：
  - 点击关灯按钮，页面变黑了
  - 点击开灯按钮，页面变白了
- 步骤：
  - **获取元素**：两个按钮
  - **注册事件**：
  - **在事件处理程序中实现你的效果**

```javascript
// 获取关灯按钮
var closeBtn = document.getElementById('close');

// 注册点击事件
closeBtn.onclick = function(){
    // 修改背景颜色
    document.body.style.backgroundColor = '#000';
};
```

- 调试：遇见没有效果了，怎么办；
  - **千万不要回去直接看代码 ！！！**
  - 看哪？看控制台，没有报错

```js
Uncaught TypeError: Cannot set property 'onclick' of null

// 未捕获的类型错误： 不能  设置  属性 'onclick' 给 null
// 说明你使用了 null 来点了 onclick  ---> 点onclic的那个玩意是null

```
#### 类样式-属性--className：DOM节点上的class**属性
- 操作类样式的效果：可以添加或修改我们已经写好的类名；更快的跟换样式；

```js
console.log(元素.class); // 输出undefined
console.log(元素.className); // 正常输出元素的class属性

// 如果要修改类样式，只需要把className修改一下就行了；
// 但是会直接覆盖
box.className = '新的类名';

// 解决：在原来的基础上进行添加类名
box.className += '新的类名';
```



#### 类样式---属性对象classList：管理着所有类名

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

- toggle：切换类名

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



### value 原有属性
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

### src

### 案例：点击按钮切换图

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
- 什么DOM节点时有这样的属性：`<input type="checkbox" name="check" class="ck" />`

```js
var ck = document.getElementById('ck');

ck.checked = true;
ck.checked = false;
```



## 案例：全选盒子

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












## 自定义属性
- **自定义属性**： 自己胡乱命名的，**没有什么功能，就是自己需要**；
- 命名: 在标签上已自定义属性 以 data-属性名
- 获取：以 data- 开头的自定义属性，都存储在了 元素.dataset 这个对象里面
  ipt.dataset.src
  事件执行函数：内部如何获取到DOM节点的自定义属性；可以通过标签，也可以通过this;


```js
<div id="box" class="abc" title="我叫div" abc="abc" data-abc="我是自定义属性" data-index="5" data-name="狗蛋"></div>

var box = document.getElementById('box');
console.log(box.id);
console.log(box.className);
console.log(box.title);
console.log(box.abc);
console.log(box.dataset);
```

 

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

 

