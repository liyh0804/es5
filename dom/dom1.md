## DOM (文档对象模型)
   功能： 描绘一个层次化的节点树，为基本的文档结构及查询提供了接口

 <html>
    <head>
        <title>Sample Page</title>
    </head>
    <body>
        <p>Hello World!</p>
    </body>
 </html>

 文档节点是每个文档的跟节点，只有一个子节点<html>

 Document
   |
   |
   |-------Element html
                |
                |--------- Element head
                |            |
                |            |------- Element title
                |                           |-------- Text Sample Page
                |
                |
                |--------- Element body
                             |
                             |------ Element p
                                        |--------- Text Hello World!


### Node 类型
    js中所有节点类型都继承自Node类型，所有节点类型都共享相同的基本属性和方法
    
    基本属性：
    nodeType属性----节点类型
    12个数值常量表示：
    Node.ELEMENT_NODE(1)
    Node.ATTRIBUTE_NODE(2)
    Node.TEXT_NODE(3)
    Node.CDATA_SECTION_NODE(4)
    Node.ENTITY_REFERENCE_NODE(5)
    Node.ENTITY_NODE(6)
    Node.PROCESSING_INSTRUCTION_NODE(7)
    Node.COMMENT_NODE(8)
    Node.DOCUMENT_NODE(9)
    Node.DOCUMENT_TYPE_NODE(10)
    Node.DOCUMENT_FRAGMENT_NODE(11)
    Node.NOTATION_NODE(12)

// 判断节点类型
```js
if (someNode.nodeType === Node.ELEMENT_NODE) {
    //... IE存在兼容性问题
}
if (someNode.nodeType === 1) {
    // 适用所有浏览器
}
```

Web浏览器，开发人员最常用的就是元素节点Node.ELEMENT_NODE(1) 和文本节点 Node.TEXT_NODE(3)

#### nodeName / nodeValue属性
```js
// 使用前先判断节点类型， 元素ELEMENT的nodeName等于标签名
if (someNode.nodeType === 1) {
    value = someNode.nodeName
}
```
每个节点都有一个childNodes属性 ----> 保存着一个NodeList对象,是一个类数组对象
```js
var firstChild = someNode.childNodes[0]
var secondChild = someNode.childNodes.item(2)
var count = someNode.childNodes.length
```

```js
function convertToArray(nodes) {
    var array = null
    try {
        array = array.prototype.slice.call(nodes, 0);
    } catch(ex) {
        array = new Array();
        for (var i = 0; i < nodes.length; i ++) {
            array.push(nodes[i])
        }
    }
    return array
}
```

parentNode  previousSibling nextSibling firstChild lastChild
hasChildNodes()
ownerDocument  --> 指向表示整个文档的文档节点

## DOM提供了操作节点的方法：
appendChild()  在childNodes末尾追加新增节点，如果该节点已经是文档一部分了，则该节点会从原来位置转移到新位置
```js
var returnedNode = someNode.appendChild(newNode)
alert(returnedNode === newNode) // true

var returnedNode = someNode.appendChild(someNode.firstNode)
alert(returnedNode === someNode.firstNode) // false
alert(returnedNode === someNode.lastNode) // true
```

节点插入childNodes具体某一位置：insertBefore(要插入的节点，作为参照的节点)  插入之后，被插入的节点会成为参照节点的前一个同胞节点previousSibling, 参照节点为null，insertBefore等同于appendChild

```js
var returnedNode = someNode.insertBefore(newNode, someNode.childNode.lastChild);
```

替换节点 replaceChild() 两个参数：要插入的节点、要替换的节点
```js
var returnedNode = someNode.replaceNode(newNode, someNode.lastNode);
```

移除节点 removeChild() 一个参数：要被移除的节点
```js
var formerLastChild = someNode.removeChild(someNode.lastChild);
```

复制节点cloneNode() :参数true、false表示深复制【节点及其整个子节点树】，浅复制【节点本身】

处理文档树中的文本节点normalize():
   某节点调用该方法，会在该节点的后代节点中查找文本节点没有文本 和 出现连续的两个文本节点的情况，将其删除或者合并

## Document
HTMLDocument ---> document
nodeType = 9
nodeName = "#document"
nodeValue = null
parentNode = null
ownerDocument = null
子节点可能是一个DocumentType、Element、ProcessingInstruction、Comment

documentElement 始终指向html页面中的<html>元素
childNodes 列表访问文档元素
```js
var html = document.documentElement
html === docuemnt.childNodes[0] === document.firstChild
```

body属性： 直接指向<body>
var body = document.body


HTMLCollection对象的一个方法： namedItem()
```js
var images = document.getElementsByTagName("img")
var myImage = images.namedItem("myImage")
```
获取整个文档所有元素：
var allElements = document.getElementsByTagName("*")

HTMLDocument特有的：getElementsByName()  :: 最常用的是取得单选按钮
<fieldset>
    <ul>
        <li> 
            <input type="radio" value="red" name="color" id="colorRed"> 
            <label for="colorRed">Red </label>
        </li>
        <li>
            <input type="radio" value="green" name="color" id="colorGreen">
            <label for="colorGreen">Green </label>
        </li>
    </ul>
</fieldset>
```js
var radios = document.getElementByName("color")
```

#### 特殊的HTMLCollection集合
document.anchors ---> 文档中所有带name特性的<a>元素
document.forms
document.images
document.links ----> 文档中所有带href特性的<a>元素

#### 文档写入
    document.write() document.writeln() document.open() document.close()

    动态加入外部资源：
    document.write("<script type=\"text/javascript\" src=\"file.js\">" +"<\/script>");




### Element类型
    提供了对元素标签名、子节点及特性的访问
    nodeType = 1
    nodeName = 元素标签名 （nodeName = tagName）
    nodeValue = null
    parentNode = Document/Element

    <div id="myDiv"></div>
    ```js
    var div = document.getElementById("myDiv")
    if (div.tagName.toLowerCase() === 'div') {
        // ...
    }
    ```
#### html元素特性
    id、title、className
    var div = document.getElementById("myDiv")

    id = div.id
    title = div.title
    className = div.className
##### 特性操作接口
    elem.getAttribute()
    elem.setAttribute()
    elem.removeAttribute()

    HTML5规范： 自定义特性，加data-前缀方便验证

    js编程操纵dom时，只使用对象的属性，代替getAttribute【取自定义属性的情况下，使用getAttribute()】

##### attributes属性
  attributes属性中包含一个NamedNodeMap, getNamedItem(name)



## Text 文本节点
    nodeType = 3
    nodeName = '#text'
    nodeValue = 节点所包含的文本
    parentNode 是一个Element
    不支持，没有子节点

    通过nodeValue、data属性访问Text节点中包含的文本
    appendData(text)
    deleteData(offset, count)
    insertData(offset, text)
    replaceData(offset, count, text)
    splitText(offset) // 从offset位置将当前文本分成两个文本节点
    substringData(offset, count)
    
    ```js
    var textNode = div.firstChild
    div.firstChild.nodeValue = "some other message"
    ```

    ### 创建文本节点
    document.createTextNode()
    ```js
    var textNode = document.createTextNode("<strong>Hello</strong> world!")

    var element = document.createElement("div")
    element.className = "message"
    element.appendChild(textNode)
    docuement.body.appendChild(element)
    element.normalize()
    ```
    分割文本节点： 是从文本节点中提取数据的一种常用DOM解析技术


## DOM操作技术

### 动态脚本
    页面加载时不存在，将来某一时刻通过DOM动态添加脚本
    <script src="xxx" type="text/javascript" />
    ```js
    function loadScript(url) {
        var script = document.createElement("script");
        script.type = "text/javascript"
        script.src = "http://xxx/xxx.js"
        document.body.appendChild(script);
    }
    ```
### 动态样式
    <link rel="stylesheet" type="text/css" href="styles.css">
    ```js
    function loadStyles(url) {
        var link = document.createElement("link")
        link.rel = "stylesheet"
        link.type = "text/css"
        link.href = url
        var head = document.getElementsByTagName("head")[0]
        head.appendChild(link);
    }
    ```

### 
