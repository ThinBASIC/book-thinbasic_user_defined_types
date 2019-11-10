## Inclusion

Sometimes you wish to re-use the elements of an existing type, but you need them at a specific location.

Using the *inclusion* mechanism, you can specify where will the element be included.

In our case, creating `Point3D` would be as done as:
```thinbasic
TYPE Point3D
  Point2D
  z AS SINGLE
END TYPE
```

In this case, `x` and `y` will be placed before `z` in the UDT memory.

Should you need to have them after `z`, just put the included type in different place:
```thinbasic
TYPE Point3D
  z AS SINGLE
  Point2D  
END TYPE
```
 
Now `z` goes first, and `x` and `y` follow. 