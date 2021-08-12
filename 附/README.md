# 附
## 实践建议
### 合并visitors
```
// bad
path.traverse({
  Identifier(path) {
    // ...
  }
});

path.traverse({
  BinaryExpression(path) {
    // ...
  }
});
//good
path.traverse({
  Identifier(path) {
    // ...
  },
  BinaryExpression(path) {
    // ...
  }
});
```
### 可以手动查找就不要遍历
特定的、浅层的节点可以手动查找而不使用traverse
### 嵌套访问时，抽离visitor function
```
// bad
const MyVisitor = {
  FunctionDeclaration(path) {
    path.traverse({
      Identifier(path) {
        // ...
      }
    });
  }
};
// good
const nestedVisitor = {
  Identifier(path) {
    // ...
  }
};

const MyVisitor = {
  FunctionDeclaration(path) {
    path.traverse(nestedVisitor);
  }
};
```
## 访问器模式

D:\personal\pattner\visitor.js