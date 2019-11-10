### \_destroy 

The optional `_destroy` function has two basic properties:
- is automatically called once the variable goes out of scope
- it does not take any parameters 

Defining it in the context of `Point2D` has no meaning, but we can use it to illustrate how it works:

```
TYPE Point2D
  x AS SINGLE
  y AS SINGLE
  
  FUNCTION _create(x AS SINGLE, y AS SINGLE)
    ME.x = x
    ME.y = y
    msgBox strFormat$("Point2D Variable is being created with x = {1}, y = {2}", ME.x, ME.y)
  END FUNCTION
  
  FUNCTION _destroy()
    msgBox "Point2D Variable is being released"
  END FUNCTION  
END TYPE

msgBox "Hello, I am about to call MyFunction"

MyFunction()

msgBox "Hello, I finished calling MyFunction"

FUNCTION MyFunction()
  DIM p AS Point2D(1, 2)
END FUNCTION
```
