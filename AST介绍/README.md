# AST介绍
## Abstract Syntax Tree
可以简单理解为描述代码的对象。
一切事物都可以转为key-value的对象结构，比如描述浏览器的BOM、文档的DOM、虚拟DOM
比如要描述`const a = 1`，我们可以创造这样的数据结构：

```
{
	type:"declaration",
	kind:"const",
	declarator:"a",
	init:1
}
```
## 起源
若干年前，Mozilla的一个工程师，创建了一个API，能够将Firefox SpiderMonkey引擎的 js 解析器暴露为JS API。

这个解析器的输出格式成为了一种通用格式流行起来，成为操作JS源代码的一个工具。

## 标准
 ESTree 指导委员会：由eslint、acorn、babel的几个成员组成
[estree](https://github.com/estree/estree)

## DEMO
`const a = 1`的AST摘要：

```
"program": {
    "type": "Program",
    "start": 0,
    "end": 25,
    "loc": {
      "start": {
        "line": 1,
        "column": 0
      },
      "end": {
        "line": 14,
        "column": 0
      }
    },
    "sourceType": "module",
    "interpreter": null,
    "body": [
      {
        "type": "VariableDeclaration",
        "start": 0,
        "end": 12,
        "loc": {
          "start": {
            "line": 1,
            "column": 0
          },
          "end": {
            "line": 1,
            "column": 12
          }
        },
        "declarations": [
          {
            "type": "VariableDeclarator",
            "start": 6,
            "end": 11,
            "loc": {
              "start": {
                "line": 1,
                "column": 6
              },
              "end": {
                "line": 1,
                "column": 11
              }
            },
            "id": {
              "type": "Identifier",
              "start": 6,
              "end": 7,
              "loc": {
                "start": {
                  "line": 1,
                  "column": 6
                },
                "end": {
                  "line": 1,
                  "column": 7
                },
                "identifierName": "a"
              },
              "name": "a"
            },
            "init": {
              "type": "NumericLiteral",
              "start": 10,
              "end": 11,
              "loc": {
                "start": {
                  "line": 1,
                  "column": 10
                },
                "end": {
                  "line": 1,
                  "column": 11
                }
              },
              "extra": {
                "rawValue": 1,
                "raw": "1"
              },
              "value": 1
            }
          }
        ],
        "kind": "const"
      }
    ],
    "directives": []
  }
```

## 工具
[ast在线转换：https://astexplorer.net/](https://astexplorer.net/)

## AST生成过程

![AST生成过程](https://img-blog.csdnimg.cn/img_convert/5cb2c784cc5842833331f4aef28619da.png)


### 词法分析

编译的第一个阶段是扫描源代码文本，scanner会从左到右扫描文本，把文本拆成一些单词。然后，这些单词传入分词器，经过一系列的识别器（关键字识别器、标识符识别器、常量识别器、操作符识别器等），确定这些单词的词性，这一过程的产物是token序列。token在机内一般用<type, value>形似的二元组来表示，type表示一个单词种类，value为属性值，比如var这个单词，在js语言里是一个关键字，一种语言的关键字集合是事先可以确定的，所以它的type本身就可表示这个关键字，不再需要属性值， 用二元组表示就是<VAR, ->；

### 语法分析

分词阶段完成以后，token序列会经过我们的解析器，由解析器识别出代码中的各类短语，会根据语言的文法规则(rules of grammar)输出解析树，这棵树是对代码的树形描述。文法是什么呢？可以参考语文中的主谓宾定状补，不同语言有自己的文法结构和规则。

## 类型
不同的语法有不同的ast类型，ast以有限的类型表述无穷的表达
### Literal字面量

![](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/29185815036a4ea1878484ba773a3b6e~tplv-k3u1fbpfcp-watermark.awebp)

### Identifier标识符

变量名、参数名、属性，可以理解为引用名

![](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/9a4b54e6512a4da7ad5c99e7a61a62e9~tplv-k3u1fbpfcp-watermark.awebp)

### Statement语句

for/switch case/if/break等等

![](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/d711045e21bb44b68495088df6a9a60b~tplv-k3u1fbpfcp-watermark.awebp)



### Declaration声明

![](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/5303fa5530944a638d6b3d1af93f0e3f~tplv-k3u1fbpfcp-watermark.awebp)



### Expression

表达式（对象和数组字面量也都是表达式）

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/feabcb940982409b911dcbb6066e8aa7~tplv-k3u1fbpfcp-watermark.awebp)

有些表达式可以单独当成语句，有些需要和其他类型节点一起构成语句

![](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/07a3f1e392f649adb764ada46ee48602~tplv-k3u1fbpfcp-watermark.awebp)

### Class

![img](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/0c62ec375157488780e2beae39e7620d~tplv-k3u1fbpfcp-watermark.awebp)

### import

![img](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/e501a0dfcce043c184e6320e22a4211c~tplv-k3u1fbpfcp-watermark.awebp)

### export

![img](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/c3ccde25491e42199088fe1f050469ab~tplv-k3u1fbpfcp-watermark.awebp)

## AST 的公共属性
- type： AST 节点的类型
