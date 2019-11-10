### Element offset

The members are stored in the memory in the order they are defined.

This is very important because it means that swapping lines of member definition will completely change the memory representation.

In order to find element byte offset, please use the dedicated *UDT_ElementOffset* function:
```thinbasic
msgBox strFormat$("Offset of .x is: {1} bytes, .y {2} bytes",
                  UDT_ElementOffset(point.x),
                  UDT_ElementOffset(point.y))
```

You can also use relevant *UDT_ElementByte* in order to find at which *byte* given element starts. 
