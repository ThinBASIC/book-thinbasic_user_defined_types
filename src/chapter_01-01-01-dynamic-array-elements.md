## Dynamic array elements

There is one single exception when UDT array does not have to be dimensioned at all. We call such arrays _dynamic_ and their usage is strictly restricted to use in conjunction with [UDT functions](chapter_01-04-02-udt-function.html), which can (re)dimension them before first use.

```
TYPE Polygon
  point() AS Point2D

  ...

END TYPE
```

Dynamic array element has then just empty brackets specified, to distinguish it from a simple element.
