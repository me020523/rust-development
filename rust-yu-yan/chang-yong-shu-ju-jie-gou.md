---
description: Rust标准库提供的常用数据结构
---

# 常用数据结构

## Vector

### 创建

```rust
let mut v = vec![1,2,3,4]; //利用vec!宏构造
let mut v2:Vec<i32> = Vec::new(); //利用new方法
```

### 访问

```rust
let t = v[0];  //当索引不存在时引发panic
let r = v.get(1);  //返回Option枚举; 当索引不存在时不引发panic
```

### 修改

```rust
v.push(24);  //追加
v[1] = 1000; //更新
```

### 迭代

```rust
for i in v {
    print!(" {} ", i)
}
```

