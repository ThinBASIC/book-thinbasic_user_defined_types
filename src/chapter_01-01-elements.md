## Elements

As the previous chapter mentioned, you need to specify at least one element for user defined type.

### Syntax
```thinbasic
[STATIC] elementName[(numberOfDimensions)] AS elementType [= value]
```

Element definition has two mandatory parts:
- *elementName*, following the same naming rules as any other variable
- *elementType*, which can be any numeric, string or user defined type

Element can be also an array, in such a case you specify number of items in the brackets after the *elementName*:

```thinbasic
TYPE Triangle
  point(3) AS Point2D
END TYPE

DIM t AS Triangle

t.point(1).x = 0 : t.point(1).y = 0
t.point(2).x = 2 : t.point(2).y = 0
t.point(3).x = 1 : t.point(3).y = 1
```

> *Note:* There is one exception, when array does not have to be dimensioned. See [Data handling functions](./chapter_01-03-data-handling-functions.md) if needed.

### Static elements
Element can be optionally marked as **static**. This means, that this field is *shared* between all the variables of given type.

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

Once you run this example, you can see that values of `x` and `y` are unique to variables `a` and `b`, however, the `description` of `a` has been promoted to `b` due to shared, static nature of the element. This connection works even in the other direction - if you change the static element in `b` now, it will be immediately reflected in `a`.

> Static elements are the only type of element to have the option of intialization.

```thinbasic
TYPE Point2D
  x AS SINGLE
  y AS SINGLE
  
  STATIC description AS STRING = "Simple 2D Point"
END TYPE

DIM p AS Point2D

msgBox p.description
```

The example will show *"Simple 2D Point"* message, because the *p* variable has the member *description* initialized in *type / end type* block.