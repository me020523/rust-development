# 面向对象编程

## 方法

struct、enum、trait可以定义方法，方法的第一个参数是self。

关键字: `impl`

```rust
#[derive(Debug)]
struct Rectangle {
    width: u32,
    height: u32,
}
impl Rectangle {
	  //不可变方法: 方法不可修改成员
    fn area(&self) -> u32 {
        self.width * self.height
    }
    fn width(&mu self, w: u32){
	    self.width = w;
    }
}
fn main() {
    let rect1 = Rectangle { width: 30, height: 50 };
    println!(
        "The area of the rectangle is {} square pixels.",
        rect1.area()
    );
}
```

## 关联函数

在`impl`块中也可以定义普通的函数，这类函数称为`关联函数`。使用这类函数需要以类型名作用为限定符。

```rust
#[derive(Debug)]
struct Rectangle {
    width: u32,
    height: u32,
}
impl Rectangle {
	  fn New() -> Rectangle {
	      Rectange{
	        width: 10,
	        height: 10,
	      }
	  }
}
fn main() {
    let rec = Rectangle::New();
}
```

## 特征\(Trait\)

Trait，类似于面向对象中的接口，定义了一组公共的函数签名。

### 定义

关键字: `trait`

```rust
pub trait Summary {
    fn summarize(&self) -> String;
}
```

### 实现

关键字: `impl`

```rust
pub struct NewsArticle {
    pub headline: String,
    pub location: String,
    pub author: String,
    pub content: String,
}
//实现Summary
impl Summary for NewsArticle {
    fn summarize(&self) -> String {
        format!("{}, by {} ({})", self.headline, self.author, self.location)
    }
}
```

### 默认实现

```rust
pub trait Summary {
    fn summarize(&self) -> String {
        String::from("(Read more...)")
    }
}
```

### 作为函数函数

```rust
pub fn notify(item: impl Summary) {
    println!("Breaking news! {}", item.summarize());
}
```

### 作为函数返回值

```rust
fn returns_summarizable() -> impl Summary {
    Tweet {
        username: String::from("horse_ebooks"),
        content: String::from("of course, as you probably already know, people"),
        reply: false,
        retweet: false,
    }
}
```

### Trait Bound

```rust
//实现一个trait
pub fn notify(item: impl Summary);
//实现多个trait
pub fn notify(item: impl Summary + Display);
```

