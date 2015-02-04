今天在啃ReactJs文档时看到这么一段话：

> It is important to remember that JavaScript does not guarantee the ordering of properties will be preserved. In practice browsers will preserve property order except for properties that can be parsed as a 32-bit unsigned integers. Numeric properties will be ordered sequentially and before other properties.

说的是，虽然JS不保证Object属性的顺序，但实际上浏览器在实现时，除了32位无符号整型外，其他的都会保留申明或添加时的顺序，而对以整型key的情况，会插入到其他属性前面，整型key之间以ascii码值排序。如：

![](/images/object-order-1.png)

若要排除整型key带来的干扰，可统一加上key前缀：

![](/images/object-order-2.png)

从此以后，可放心地依赖Object的顺序啦~