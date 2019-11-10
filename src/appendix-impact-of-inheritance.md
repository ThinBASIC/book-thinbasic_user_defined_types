### Impact of inheritance

You need to keep in mind that many low level languages do not offer UDT inheritance equivalent.

In such case, you need to "flatten" the UDT to its final form:

With this knowledge, you may translate thinBASIC `Point3D` this way:
```
TYPE Point2D
  x AS SINGLE
  y AS SINGLE
END TYPE

TYPE Point3D EXTENDS Point2D
  z AS SINGLE
END TYPE
```

...as the following in C:
```c
struct Point3D {
  float x;
  float y;
  float z;
};
```

...as the following in Rust:
```rust
struct Point2D {
  pub x: f32,
  pub y: f32,
  pub z: f32,
}
```