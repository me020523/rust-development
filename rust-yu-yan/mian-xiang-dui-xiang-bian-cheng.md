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



