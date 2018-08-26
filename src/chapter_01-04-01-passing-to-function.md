### Passing to function

UDT variables can be passed to any function - by value or by reference.

As the UDT's represent a group of multiple other types, their memory footprint can be larger.

As with all other variables, `byRef` is faster, while `byVal` ensures the value does not get altered.

General rules of thumb:
- if changing the UDT variable from function is wanted or no issue, always use `byRef`
- if you know you will not change the value in function, always use `byRef` 
- in all the other cases use `byVal`, it will ensure the UDT variable value will not change

Little example to illustrate the difference.
```thinbasic
TYPE Point2D
  x AS SINGLE
  y AS SINGLE
END TYPE

DIM point AS Point2D
```

Here we have our `Point2D` example again.

Imagine you want to change the element values via function. You can do it like:
```
Point2DSetXY(point, 1, 2)

SUB Point2DSetXY(byRef point AS Point2D, x AS SINGLE, y AS SINGLE)
  point.x = x
  point.y = y
END SUB
```

ByRef is wanted here, this function is explicitly designed to change the element values.

Another example:
```thinbasic
msgBox Point2DAsString(point)

FUNCTION Point2DAsString(byRef point AS Point2D) AS STRING
  RETURN strFormat$("[{1}, {2}]", point.x, point.y)
END FUNCTION
```

ByRef is safe to use here, because we use it just to make the function call faster.
The value of `Point2D` is not altered here, just read.

And last, but not least:
```thinbasic
SINGLE halfSum = Point2DGetSumOfHalfs(point)

FUNCTION Point2DGetSumOfHalfs(byVal point AS Point2D) AS SINGLE
  point.x /= 2
  point.y /= 2
  
  RETURN point.x + point.y
END FUNCTION
```

ByVal is needed, as you need to modify the variable for purpose of the calculation, but do not want to change the original variable.
