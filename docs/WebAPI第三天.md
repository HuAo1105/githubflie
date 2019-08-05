## 创建节点

* document.createElement：根据指定的标签名，创建一个新的元素；

```js
document.createElement('标签名');

// 该方法创建的元素，是不会自动进入结构里面的，需要自己手动添加
```

## 修改节点的内容

```js
// innerText：用于获取或者设置某个元素里面的文本内容，不具备解析HTML结构；
li.innerText = '内容';
```

## 通过节点的获取

```js
ul.children[0]
```

## 添加节点

* appendChild：给一个父元素，追加子元素，**作为最后一个子元素**；**从后添加一个子元素**
* insertBefore：在某个子元素之前，插入新的子元素

```js
// 父元素.insertBefore(新的子元素,旧的子元素)
var second = document.querySelector('.second');
ul.insertBefore(li,second);
```

## 根据DOM节点 获取 DOM节点

* 获取子元素：可以得到某个元素之下的所有的子元素的集合，一个**伪数组**

```js
父元素.children
```

* 获取父元素

```
元素.parentNode
```

* 获取兄弟元素

```
元素.nextElementSibling  -  得到下一个兄弟元素
元素.previousElementSibling - 得到上一个兄弟元素
```

## 删除节点

```js
删除的是父元素下的某个子元素

// 父元素.removeChild(要删除的子元素);

var first = ul.children[0];
// 调用方法，移除
ul.removeChild(first);
```

# BOM

* 浏览器对象：**window对象**
* window特点：
  * 特点因为window对象在浏览器中被称为顶级对象，所谓的**顶级对象**，是指：页面中所有的东西都是依赖于这个对象存在的
  * 所有的全局变量和全局函数都是window对象的属性和方法

## onload

* 页面加载完毕：页面所需的静态资源全部加载完毕

## 定时器

* setTimout：一次性定时器；set - 设置；Timeout - 超时

```js
// 作用： 延迟一定的毫秒之后，调用函数一次
// 返回值： 是该定时器的id，可以用于停止这个定时器
var timer = setTimout(函数,延迟的毫秒数)

// 停止一次性的定时器：清除后，就不会执行这个定时器；
clearTimeout(timer)
```



* setInterval：永久性的定时器；interval - 间隔

```js
// 作用：阶段的时间执行函数；
// 返回值：就是该定时器的id
var timer = setInterval(函数,间隔);

// 清除永久定时器
clearInterval(timer);
```



## location

```js
// 如果想要使用js进行跳转，只需要 location.href = 新的地址;
location.href = 'http://www.jd.com';
```

## localStorage和JSON

### localStorage

```js
// 存储 设在存上一条数据
// 后面的值 前面可以放入任何数据类型，保存后为字符串
// 注意： 如果存储的是对象之类的复杂类型，需要先把复杂类型转换为JSON格式的字符串，再存进去，因为本地存储只能存储字符串
localStorage.setItem(键,值);

// 读取数据
// 返回值：就是我们存入的的数据的值
localStorage.getItem(键);
```

### json

```js
// 将对象转换为json格式的字符串
// 返回值：一个满足json格式的 字符串
JSON.stringify(对象)

// 将json格式的字符串转换为对象
// 返回值：依赖于你的json格式字符串，可能返回数组，或者是对象....
JSON.parse(json格式字符串)
```









