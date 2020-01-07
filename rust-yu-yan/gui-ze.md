---
description: Rust通过一些编程规则解决语言的安全问题
---

# 规则

## Borrowing

#### 1. 在同一个作用域\(通过'{}'划分\)，同一个值最多只能有一个可变引用。

在编译期解决值的竞态问题。non-lexical lifetimes可以优化编程体验。

