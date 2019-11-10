### Comparative data types

ThinBASIC uses BASIC convention for data type naming, which is incompatible with most non-BASIC languages.

The following table will help you with matching the correct thinBASIC type with the correct type in the targetted language:
<table>
    <tr><th>Data type</th><th>Meaning</th></tr>
    <tr><td>INTEGER</td><td>16 bit signed integer</td></tr>
    <tr><td>LONG</td><td>32 bit signed integer</td></tr>
    <tr><td>QUAD</td><td>64 bit signed integer</td></tr>    
    <tr><td>BYTE</td><td>8 bit unsigned integer</td></tr>
    <tr><td>WORD</td><td>16 bit unsigned integer</td></tr>
    <tr><td>DWORD</td><td>32 bit unsigned integer</td></tr>
    <tr><td>SINGLE</td><td>32 bit floating point</td></tr>
    <tr><td>DOUBLE</td><td>64 bit floating point</td></tr>
    <tr><td>EXTENDED</td><td>80 bit floating point</td></tr>
    <tr><td>NUMBER</td><td>80 bit floating point</td></tr>
    <tr><td>STRING</td><td>BSTR</td></tr>
    <tr><td>ASCIIZ</td><td>Null-terminated buffer of characters</td></tr>
</table>

With this knowledge, you may translate thinBASIC UDT:
```
TYPE Point2D
  x AS SINGLE
  y AS SINGLE
END TYPE
```

...as the following in C:
```c
struct Point2D {
  float x;
  float y;
};
```

...as the following in Rust:
```rust
struct Point2D {
  pub x: f32,
  pub y: f32,
}
```
