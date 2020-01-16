# 泛型\(Generic\)

## 函数

```rust
fn largest<T>(list: &[T]) -> T {
    //函数定义
}

//隐式推导类型
let number_list = vec![34, 50, 25, 100, 65];
let max = largest(&number_list);

//显示声明类型
```

## 结构体

```rust
struct Point<T> {
    x: T,
    y: T,
}
//隐匿推导类型
let integer = Point { x: 5, y: 10 };
```

## 枚举

```rust
enum Result<T, E> {
    Ok(T),
    Err(E),
}
```

## 方法

```rust
struct Point<T, U> {
    x: T,
    y: U,
}

impl<T, U> Point<T, U> {
    fn mixup<V, W>(self, other: Point<V, W>) -> Point<T, W> {
        Point {
            x: self.x,
            y: other.y,
        }
    }
}
```

## 特征\(Trait\)

### +语义

```rust
use std::fmt::Display;

struct Pair<T> {
    x: T,
    y: T,
}

impl<T> Pair<T> {
    fn new(x: T, y: T) -> Self {
        Self {
            x,
            y,
        }
    }
}

impl<T: Display + PartialOrd> Pair<T> {
    fn cmp_display(&self) {
        if self.x >= self.y {
            println!("The largest member is x = {}", self.x);
        } else {
            println!("The largest member is y = {}", self.y);
        }
    }
}
```

### where语义

```rust
fn some_function<T: Display + Clone, U: Clone + Debug>(t: T, u: U) -> i32 {
    //
}
```



