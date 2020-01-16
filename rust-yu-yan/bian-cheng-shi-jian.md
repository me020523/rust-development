# 编程实践

## Borrow

### Cannot move out of borrowed content

```rust
fn ref_copy() {
    let p = Point{a:10,b:10};
}

fn ref_copy_internal(v:&Point) -> Point{
    *v;   //compiler panic, cannot move out borrowed content
}
```

### Cannot move out of type '\[T; x\]', a non-copy array.

```rust
fn array_elem_ownership() {
    let nums = [1,2,3,4,5];
    array_elem_ownership_internal(nums[3]); //just copy
    println!("{}",nums[3]);

    let points = [
        Point{a:1, b:2},
        Point{a:1, b:2},
    ];

    let p = points[0];  //compiler panic, non-copy array
}
```

数组中的元素不能发生归属权的迁移，传递数组中的元素要么采用复制，要么采用borrow.



