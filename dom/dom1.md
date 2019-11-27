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