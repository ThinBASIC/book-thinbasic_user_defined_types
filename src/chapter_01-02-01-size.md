#### Size
In order to determine the size of UDT in memory, alway use dedicated functions.

*SizeOf* will tell you how much memory is occupied by UDT. You can use it both with UDT or UDT variable:
```thinbasic
msgBox SizeOf(Point2D)

DIM point AS Point2D

msgBox SizeOf(point)
```

Both of these will return `8` in this case, because UDT has two *single precision* members, each occupying 4 bytes.

How can you get this detailed information for members? Use SizeOf directly on them:
```thinbasic
msgBox strFormat$("Size of .x is: {1} bytes, .y {2} bytes",
                  SizeOf(point.x),
                  SizeOf(point.y))
```

> Please note the dynamic STRING always occupies 4 bytes, because it is internally represented via pointer.
