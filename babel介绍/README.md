# babel介绍

## 巴别塔

babel名字来源于巴别塔，也叫通天塔。

《圣经·旧约·创世记》记载：当时人类联合起来兴建希望能通往天堂的高塔；为了阻止人类的计划，上帝让人类说不同的语言，使人类相互之间不能沟通，计划因此失败，人类自此各散东西。此事件，为世上出现不同语言和种族提供解释。


## babel编译流程
![babel编译流程](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/ee9eaa1f265c4c49ad156f2c691748d9~tplv-k3u1fbpfcp-watermark.awebp)

**parse**：将代码转为AST
babel使用的解析器是**babylon**，后更名为 **@babel/parser**，而babylon是基于**acorn**（目前UglifyJS的js解析器也是基于acorn，也有其他的解析器，比如typescript）

**transform**：对AST进行操作（遍历、修改、替换）

**generate**：将AST转为代码
