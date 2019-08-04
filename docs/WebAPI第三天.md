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

## 添加节点

* appendChild：给一个父元素，追加子元素，**作为最后一个子元素**；**从后添加一个子元素**
* insertBefore：在某个子元素之前，插入新的子元素

```js
// 父元素.insertBefore(新的子元素,旧的子元素)
var second = document.querySelector('.second');
ul.insertBefore(li,second);
```

