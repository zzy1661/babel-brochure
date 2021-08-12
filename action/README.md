# 实战

## 目标
支持在注释中使用@mock进行mock测试
```
/**
 * 查询结算单
 * @param {*} options
 * @returns
 * @mock {code: 1,message: "查询成功",result:{pageIndex: 1,pageSize: 10,total: "1","result|5":[{id:'@integer',salesbillNo: "PN@integer",amountWithTax: "6.000000",taxAmount: "0.000000"}]}}
 */
export async function queryBillPage(options) {
  const res = await billFetch.post({
    url: API.queryBillPage,
    data: {
      ...options,
    },
  });

  return res;
}
```

## 思路
这个代码是自动生成的，有两个规律：
`export function`和`const res = await `
确定这两个的ast node type，再进行操作,将 res = 后面的内容(init)替换为 `Promise.resolve(Mock.mock(@mock内容))`

代码：
D:\work\xforceplus-mobile-ant-fe\src\services\settlement\index.js

插件：
D:\work\xforceplus-mobile-ant-fe\extentions\CommentMockPlugin.js

效果：
http://localhost:9000/ant/settlement