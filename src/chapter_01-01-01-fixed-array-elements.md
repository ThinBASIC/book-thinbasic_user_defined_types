## Fixed array elements
An element can be also an array, in such a case you specify its subscripts in the brackets after the *elementName*:

```thinbasic
TYPE Triangle
  point(3) AS Point2D
END TYPE

DIM t AS Triangle

t.point(1).x = 0 : t.point(1).y = 0
t.point(2).x = 2 : t.point(2).y = 0
t.point(3).x = 1 : t.point(3).y = 1
```

Element arrays defined this way can have up to 3 dimensions, with the number of items in each dimension separated by comma.

```thinbasic
TYPE ConsoleScreen
  character(80, 25) AS STRING * 1
END TYPE

DIM cs AS ConsoleScreen

cs.character(1, 1) = "a"
```
