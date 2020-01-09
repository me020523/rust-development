---
description: 重载(不)相等、比较运算符
---

# 相等和比较

## 相等性

* `PartialEq`
* `Eq`

`PartialEq` 实现该Trait可以重载`==`和`!=`运算符。`Eq`实现该Trait将类型标记为全序关系

## 比较

* `PartialOrd`
* `Ord`

`PartialOrd`实现该Trait可以重载: `>`,`>=`, `<`, `<=`运算符。

