---
description: Rust原生支持的数据类型
---

# 内置类型

## 整型

| Length | Signed | Unsigned |
| :--- | :--- | :--- |
| 8-bit | `i8` | `u8` |
| 16-bit | `i16` | `u16` |
| 32-bit | `i32` | `u32` |
| 64-bit | `i64` | `u64` |
| 128-bit | `i128` | `u128` |
| arch | `isize` | `usize` |

### 字面量

| Number literals | Example |
| :--- | :--- |
| Decimal | `98_222` |
| Hex | `0xff` |
| Octal | `0o77` |
| Binary | `0b1111_0000` |
| Byte \(`u8` only\) | `b'A'` |

## 浮点型

`f32`、`f64`

## 布尔型

`bool`; `true` ，`false` 

## 字符型

`char`

### 定义

```rust
fn main() {
    let c = 'z';
    let z = 'ℤ';
    let heart_eyed_cat = '😻';
}
```

## 元组\(Tuple\)

1. 元组的长度固定，一旦声明，运行时不可以扩容和缩容
2. 元组可以包含不同数据类型的值

### 定义

```rust
let tup: (i32, f64, u8) = (500, 6.4, 1);   //显式声明类型
let tup = (500, 6.4, 1); //隐式推导类型
```

### 访问

```rust
fn main() {
    let x: (i32, f64, u8) = (500, 6.4, 1);
    let five_hundred = x.0; //x.0取第一个值
    let six_point_four = x.1; //x.1取第二个值
    let one = x.2; //x.2取第三个值
}
```

### 解构\(Destructuring\)

```rust
fn main() {
    let tup = (500, 6.4, 1);
    let (x, y, z) = tup;

    println!("The value of y is: {}", y);
}
```

## 数组\(Array\)

1. 数组长度固定，一旦声明，运行时不可以扩容和缩容
2. 数组中的值类型相同

### 定义

```rust
let a: [i32; 5] = [1, 2, 3, 4, 5];  //显式定义
let a = [1, 2, 3, 4, 5]; //隐式推导

let a = [3; 5]; //语法糖. 定义大小为5的数组，初始值是3.
```

### 访问

```rust
fn main() {
    let a = [1, 2, 3, 4, 5];

    let first = a[0];
    let second = a[1];
    
    a[1]=100;
}
```

## 指针

## Slice

代表collection变量的一段切片，实现方式类似动态数组，不同数据类型的slice类型定义:

| 类型 | slice |  |
| :--- | :--- | :--- |
| 整型 | \[i8\], \[u8\], \[i16\]... |  |
| 浮点型 | \[f32\], \[f64\] |  |
| 布尔型 | \[bool\] |  |
| 字符型 | \[char\] |  |
| 字符串 | str |  |
| 自定义类型T | \[T\] |  |

* 无法声明创建slice类型的变量，因为不能在编译期确定变量值的内存大小

```rust
let mut x = [1, 2, 3];
let x = x[..]; //编译器报错
```

* slice只能使用引用类型，包含可变引用和不可变引用

```rust
let mut x = [1, 2, 3];
let x = &mut x[..]; // 创建可变引用
x[1] = 7;
let y = &x[..];  //创建不可变引用
```

* 字符串字面量是slice引用类型&str

