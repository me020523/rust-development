---
description: 模式匹配主要用在match和if let结构，方便控制代码结构。模式支持组合运算
---

# 模式匹配

## 字面量

普通的字面量作为模式，类似于常规的switch结构。

问题: 字面量的数据类型支持哪些

```rust
let x = 1;
match x {
    1 => println!("one"),
    2 => println!("two"),
    3 => println!("three"),
    _ => println!("anything"),
}
```

## 带参数的枚举

当枚举值带参数时，参数的类型和值都需要满足

```rust
fn main() {
    let x = Some(5);
    let y = 10;

    match x {
        Some(50) => println!("Got 50"), //匹配枚举类型Some，参数值是50且类型是i32
        Some(y) => println!("Matched, y = {:?}", y), //匹配枚举类型Some，参数类型是i32, y绑定参数值
        _ => println!("Default case, x = {:?}", x),  //匹配所有值，类似于default
    }

    println!("at the end: x = {:?}, y = {:?}", x, y);
}
```

## OR匹配

模式支持`|`运算符，语义是`OR(或)`，匹配任意一项

```rust
let x = 1;

match x {
    1 | 2 => println!("one or two"),  //匹配1或2
    3 => println!("three"),
    _ => println!("anything"),
}
```

## 范围匹配

运算符`..=`定义一个范围。仅支持数字类型\(integer, float\)和char类型

```rust
let x = 5;

match x {
    1..=5 => println!("one through five"),  //定义区间[1,5]的整数
    _ => println!("something else"),
}
```

## 条件匹配

```rust
let num = Some(4);

match num {
    Some(x) if x < 5 => println!("less than five: {}", x),
    Some(x) => println!("{}", x),
    None => (),
}
```

## 解构

模式支持匹配复杂数据类型的部分值。解构匹配支持嵌套。

### struct类型

```rust
fn main() {
    let p = Point { x: 0, y: 7 };

    match p {
        Point { x, y: 0 } => println!("On the x axis at {}", x), //匹配Point类型，且y值是0, x绑定Point.x的值
        Point { x: 0, y } => println!("On the y axis at {}", y), //匹配Point类型，且x值是0, y绑定Point.y的值
        Point { x, y } => println!("On neither axis: ({}, {})", x, y), //匹配Point类型, x, y绑定Point.x, Point.y的值
    }
}
```

### Enum类型

```rust
enum Message {
    Quit,
    Move { x: i32, y: i32 },
    Write(String),
    ChangeColor(i32, i32, i32),
}

fn main() {
    let msg = Message::ChangeColor(0, 160, 255);

    match msg {
        //匹配Quit
        Message::Quit => {
            println!("The Quit variant has no data to destructure.")
        },
        //匹配Move { x: i32, y: i32 }，可以定义类似struct的匹配规则
        Message::Move { x, y } => {
            println!(
                "Move in the x direction {} and in the y direction {}",
                x,
                y
            );
        }
        //匹配Write(String)，可以匹配具体参数值
        Message::Write(text) => println!("Text message: {}", text),
        //匹配ChangeColor(i32, i32, i32)，可以匹配tuple元素
        Message::ChangeColor(r, g, b) => {
            println!(
                "Change the color to red {}, green {}, and blue {}",
                r,
                g,
                b
            )
        }
    }
}
```

## 语法糖

### 忽略值

```rust
fn foo(_: i32, y: i32) {
    println!("This code only uses the y parameter: {}", y);
}

fn main() {
    foo(3, 4);
}
```

### 忽略部分值

```rust
let numbers = (2, 4, 8, 16, 32);

match numbers {
    (first, _, third, _, fifth) => {
        println!("Some numbers: {}, {}, {}", first, third, fifth)
    },
}
```

### 忽略未使用变量

```rust
fn main() {
    let _x = 5;
    let y = 10;
}
```

### 忽略剩余部分值

```rust
struct Point {
    x: i32,
    y: i32,
    z: i32,
}

let origin = Point { x: 0, y: 0, z: 0 };

match origin {
    Point { x, .. } => println!("x is {}", x),
}
```

### 创建变量

```rust
enum Message {
    Hello { id: i32 },
}

let msg = Message::Hello { id: 5 };

match msg {
    Message::Hello { id: id_variable @ 3..=7 } => {
        println!("Found an id in range: {}", id_variable)
    },
    Message::Hello { id: 10..=12 } => {
        println!("Found an id in another range")
    },
    Message::Hello { id } => {
        println!("Found some other id: {}", id)
    },
}
```



