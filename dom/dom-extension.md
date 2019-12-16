# DOM扩展

## 选择符API
    getElementById()、getElementByTagName()
    通过Document及Element类型的实例调用它们

    Selectors API Level 1的核心方法： querySelector() 、 querySelectorAll()
      ---> 通过Document、Element类型的实例调用它们

### querySelector()方法
    接收CSS选择符， 返回与该模式匹配的第一个元素， 未找到返回null
    
    ```js
    var body = document.querySelector("body")
    var img = document.body.querySelector("img.button")
    ```

### querySelectorAll()方法
    接收CSS选择符， 返回所有匹配的元素【NodeList对象】
    ```js
    var strongs = document.querySelectorAll("p strong")
    for(var i = 0, len = strongs.length; i < len; i ++) {
        strong = strongs[i] // strongs.item(i)
    }
    ```

### matchesSelector()方法  ---- 此方法不常用
    ```js
    if (document.body.matchesSelector("body.page1")) {
        // true
    }
    ```

### 元素遍历
    DOM元素添加5个属性：(去除掉了文本元素和注释)
    childElementCount:
    firstElementChild:
    lastElementChild:
    previousElementSibling:
    nextElementSibling:


## HTML5
1、getElementsByClassName()
```js
var allCurrentUsernames = document.getElementsByClassName("username current")
var selected = document.getElementById("myDiv").getElementsByClassName("selected")
```
方便的为带有某些类的元素添加事件处理程序

2、 classList

add(value) / contains(value) / remove(value) / toggle(value)

```js
div.classList.remove("user")
for(var i = 0, len = div.classList.length; i < len; i ++) {
    doSomething(div.classList[i])
}
``` 

3、焦点管理
document.activeElement属性，-----> 始终会引用DOM中当前获得了焦点的元素
元素获得焦点的方式： 页面加载、用户输入（tab）、代码中调用focus()方法

document.hasFocus() 确定文档是否活动焦点

文档加载期间， document.activeElement = null; 文档加载完成，document.activeElement = document.body

```js
var button = document.getElementById("myButton");
button.focus()
document.activeElement === button
document.hasFocus()
```

### HTMLDocument的变化
1、readyState属性
loading: 文档正在加载
2、complete: 文档已加载完成
```js
if (document.readyState  ==== 'complete') {
    // ...
}
```

2、兼容模式
document.compatMode 
取值：["CSS1Compat", "BackCompat"]标准模式、混杂模式

3、head属性
document.head ---> 对<head>的引用
实现document.head属性的浏览器包括Chrome、Safari
```js
var head = document.head || document.getElementsByTagName("head")[0]
```

4、字符集属性charset 
    通过meta、响应头部、直接设置charset修改
    document.charset = "UTF-8"
    document.defaultCharset

5、html5自定义数据属性
    data-
    // <!-- <div id="myDiv" data-appId="1234" data-appName="nochos"></div> -->
    自定义属性可以通过元素的dataset属性访问
    ```js
    var div = document.getElementById("myDiv")
    var appId = div.dataset.appId
    var myName = div.dataset.myName

    div.dataset.appId = 234234
    ```

6、插入标记技术
    innerHTML
    outerHTML
    insertAdjacentHTML


7、scrollIntoView() 方法
    document.forms[0].scrollIntoView();

8、children属性
    element.children[0]

9、contains() 方法

10、innerText/ outerText

11、滚动
    

