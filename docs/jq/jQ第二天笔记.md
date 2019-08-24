## jQ属性操作

### 设置或获取元素固有属性prop()

* 写法：$('img').prop('src')
* 写一个值，获取
* 写两个值，设置

### 设置或获取自定义属性attr()

* 写法：$('img').attr('')
* 写一个值，获取
* 写两个值，设置

> prop和attr是用来操做html属性，而不是css属性

> js里面使用lis.[i].index = i;
>
> jQ里面可以通过attr加上自定义属性

### :checked 选择器

* 查找**被选中**的表单元素

### checked

* 在jq里checked是一个固有属性，给他设置值的话，设置布尔值true或false

### jQ内容文本值

#### hmtl()

* html()            获取元素的内容
* html(’内容‘)   设置元素的内容       

#### text()

* text()             获取元素的文本内容
* text(’内容‘)    设置元素的文本内容

#### val()

* val()              获取表单的值
* val('内容')     设置表单的值

```
html()和text()一般是在双标签的时候使用表单使用val()
```

### 寻找父级的问题

* parents(' 具体哪个父元素的类名')

### jQ元素操作

> 主要是遍历、创建、添加、删除元素操作

**遍历元素**

jQuery 隐式迭代是对同一类元素做了同样的操作。如果想要给同一类元素做不同操作，就需要用到遍历。

> 语法1：$('div').each(function(index,ele) {  } )

```
1、index和ele是随意取名的，index是每个元素的索引值，ele是遍历的内容

2、遍历时，第二个参数ele是每个DOM元素对象，不是jquery对象

3、所以要想使用jquery方法，需要给这个dom元素转换为jquery对象  $(ele)

4、遍历元素
```

> 语法2：$each.(object，fuction(index,ele)  {     } )

```
1、遍历数据，object这遍历谁就写谁

2、index是每个元素的索引值，ele是遍历的内容
```

**创建元素**

> 语法：$('<li>这可以写内容</li>')

**添加到内部元素**

> element.append('内容')（把内容放入匹配元素内部最后面，
>
> element.prepend('内容')（把内容放入匹配元素内部最前面）
>
> $('<li>这可以写内容</li>').appendTo( ul ),将这个插入到ul的后边。

```
生成之后，形成父子关系
```

**外部添加**

> element.after('内容')   把内容放到目标元素后面
>
> element.before('内容')   把内容放到目标元素的前面

```
生成之后，形成兄弟关系
```

**删除元素**

> element.remove()    删除匹配的元素（本身）
>
> element.empty()       删除匹配的元素集合中所有的子节点
>
> element().html('')       清空匹配元素的内容

```js
①remove 删除元素本身。

②empt() 和  html('''') 作用等价，都可以删除元素里面的内容，只不过 html 还可以设置内容。
```

### jQ尺寸、位置操作

#### jQ尺寸

> width()、height() 【只计算宽和高】
>
> innerWidth()、innerHeight()   【包含padding + width】
>
> outerWidth()、outerHeight()  【包含padding、border、width】
>
> outerWidth(true)、outerHeight(true) 【包含padding、border、margin、width】

```
以上参数为空，则是获取相应值，返回的是数字型。

如果参数为数字，则是修改相应值。

参数可以不必写单位。
```

#### jQ位置

> 位置主要有三个：offset()、position()、scrollTop()/scrollLeft()

**offset()设置或获取元素偏移**

* offset：距离文档的距离【left、top】

```
1、offset()  方法设置或返回被选元素相对于文档的偏移坐标，和父级没有关系

2、元素.offset().left，用于获取距离文档左侧的距离；元素.offset().top，用于获取距离文档顶部的距离

3、可以设置元素的偏移：offset({
  left:50,
  top:50,
})
```

### jq注册多个事件

* on方法：可以绑定多个事件（优势1）

  * 如果是处理相同程序的事件

  ````
  $("div").on('click mouseover mouseout',function ( ) { })

  多个事件中间用空格隔开
  ````

  * 如果是处理不同的程序的事件

  ```
  $("div").on({
    mouseover:,
    click:,
  })
  ```

  * 优势2：可以事件委托操作

  ```js
  $("ul").on('click', 'li', fuction () {
    
  })
  ```

  * 优势3：动态创建的事件，click()没有办法绑定事件，on()可以给动态生成的元素绑定事件

```
eg:微博发布评论时，就相当于创建了一个动态元素，绑定事件时就要用到on绑定事件	
```

### 解绑事件

* $("div").off()              把事件全部解绑
* $('div').off('click')      只解绑click事件
* $("ul").off('click','li')   将委托给ul的li解绑

> 如果有的事件只想触发一次，可以使用one()来绑定事件

### 自触发事件trigger()

> 有些事件希望自动触发, 比如轮播图自动播放功能跟点击右侧按钮一致。可以利用定时器自动触发右侧按钮点击事件，不必鼠标点击触发

> element.click() // 第一种简写格式

> element.trigger('type') // 第二种自动触发模式

```js
$("p").trigger("click"); // 此时自动触发点击事件，不需要鼠标点击
```

> element.triggerHandler(type)  // 第三种自动触发模式

> triggerHandler模式不会触发元素的默认行为，例如：触发事件，文本框不会获取光标焦点；这是和前面两种的区别。

### jQ事件对象

> e，事件对象

```js
阻止默认行为：return false / event.preventDefault()
```



position()获取元素偏移**

> 1、posotion() 方法用于返回备选元素相对于带有定位的父级偏移坐标，如果父级都没有定位，则以文档为准
>
> 2、该方法也是有两个属性。position().top 用于获取距离定位父级元素顶部的距离；position.left()用于获取距离定位父级左侧的距离
>
> **注意**:该方法只能获取



**scrollTop()、scrollLeft()**

> scroll为事件，谁有滚动条加给谁，除了window

> 获取元素被卷进去的头部和左侧

```
1、scroll方法设置或被选元素被卷进去的头部

2、不跟参数是获取，参数为不带单位的数字则是设置被卷进去的头部

```

**补充**

* document不是元素，不能加动画
* 加动画，是加给元素的，把body和html都写上，因为有的浏览器识别的元素不一样
* scrollTop()在jq是方法
* scrollTop在js是属性
* 发布微博时，内容为空不发布，拿内容的长度来判断

### 保留小数写法

* toFixed(n),n指的是保留的小数位数

### break和return

* return是给函数用的
* break是给语句用的 






offset和scrolltop