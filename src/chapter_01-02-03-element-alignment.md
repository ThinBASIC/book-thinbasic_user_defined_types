### Element alignment

By default, the elements are tightly aligned in memory, one after each other.

> This approach is memory efficient, yet in some cases, you need an alternative:
> - when in need of optimizing UDT element access speed from low-level code
> - for compatibility with another language

You can control the alignment via the *alignment modifier*. It can take 3 different values:
- *byte*, for 1 byte alignment (default)
- *word*, for 2 byte alignment
- *dword*, for 4 byte alignment

In case you want to elements aligned to 4 byte steps, you might consider using `DWORD` modifier.

Let's have a look at this example:
```thinbasic
TYPE RGBColor
  R AS BYTE
  G AS BYTE
  B AS BYTE  
END TYPE
```

By default, the size of `RGBColor` will be 3 bytes, as you can verify with *SizeOf*:
```thinbasic
msgBox SizeOf(RGBColor)
```

3 elements, each 1 byte in size.

To apply 32bit alignment, use DWORD modifier:
```thinbasic
TYPE DwordAlignedRGBColor DWORD
  R AS BYTE
  G AS BYTE
  B AS BYTE  
END TYPE
```

This means that `R`, `G` and `B` elements will still be of *byte* data type, however, their element offset will change to 4 byte jumps.

You can verify it easily:
```thinbasic
DIM colorNormal  AS RGBColor

msgbox strFormat$("The offset of .R is {1}, .G is {2} and .B is {3}",
                  UDT_ElementOffset(colorNormal.r),
                  UDT_ElementOffset(colorNormal.g),
                  UDT_ElementOffset(colorNormal.b))

DIM colorAligned AS DwordAlignedRGBColor
                  
msgbox strFormat$("The offset of .R is {1}, .G is {2} and .B is {3}",
                  UDT_ElementOffset(colorAligned.r),
                  UDT_ElementOffset(colorAligned.g),
                  UDT_ElementOffset(colorAligned.b))
```
