## Static elements
An element can be optionally marked as **static**. This means, that this field is *shared* between all the variables of a given type.

```thinbasic
TYPE Point2D
  x AS SINGLE
  y AS SINGLE
  
  STATIC description AS STRING
END TYPE

DIM a AS Point2D
a.x = 1 : a.y = 2
a.description = "simple 2D point"
msgBox strformat$("[{1}, {2}] is {3}", a.x, a.y, a.description)

DIM b AS Point2D
b.x = 3 : b.y = 4

msgBox strformat$("[{1}, {2}] is {3}", b.x, b.y, b.description)
```

Once you run this example, you can see that values of `x` and `y` are unique for each `a`, `b` variables.

However, the `description` of `a` has been promoted to `b` due to the shared, static nature of the element.

This connection works even in the other direction - if you change the static element in `b` now, it will be immediately reflected in `a`.

STATIC elements are the only type of element, which can be initialized in the declaration:
```thinbasic
TYPE Point2D
  x AS SINGLE
  y AS SINGLE
  
  STATIC description AS STRING = "simple 2D point"
END TYPE
```

Non-static elements are always initialized to 0 (for numeric elements) or "" (for string elements).
