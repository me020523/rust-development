---
description: Rust支持struct和enum两种自定义类型
---

# 自定义类型

## 结构体\(struct\)

### 定义

关键字: `struct`

```rust
struct User { 
	username: String, 
	email: String, 
	sign_in_count: u64, 
	active: bool, 
}
```

### 初始化

#### 常规

```rust
let user1 = User {
    email: String::from("someone@example.com"),
    username: String::from("someusername123"),
    active: true,
    sign_in_count: 1,
};
```

#### 同名形参

```rust
fn build_user(email: String, username: String) -> User {
    User {
        email,
        username,
        active: true,
        sign_in_count: 1,
    }
}
```

#### 利用其它实例初始化剩余成员

```rust
let user2 = User {
    email: String::from("another@example.com"),
    username: String::from("anotherusername567"),
    ..user1
};
```

### 匿名结构体

使用tuple可以定义字段匿名的struct

```rust
struct Color(i32, i32, i32);
struct Point(i32, i32, i32);
let black = Color(0, 0, 0);
let origin = Point(0, 0, 0)
```

### 空结构体

定义不包含任何成员的空结构体

```rust
struct Empty{}
struct Empty()
```

