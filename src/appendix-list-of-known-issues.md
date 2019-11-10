# List of known issues

As thinBASIC formal checking is currently under careful research, it might be useful for you to know about the current limitations of the language, which might otherwise confuse you.

## SWAP
This useful command for swapping variable content is silently accepting UDT variable or member as a parameter, but it does not perform any action.

> **DANGER:** - missing functionality silently ignored, [reported](https://www.thinbasic.com/community/project.php?issueid=564)

## Direct assignment
While this is not an issue, it is good to know about how does this work.

When you perform the assignment of one UDT variable to another UDT variable, a copy of data is performed.

```thinbasic
TYPE Point2D
  x AS SINGLE
  y AS SINGLE
END TYPE

dim a as Point2D
a.x = 1

dim b as Point2D
b.x = 2

a = b

MSGBOX 0, a.x
MSGBOX 0, b.x
```

Please note thinBASIC currently allows you to assign two totally different types, as it performs a memory copy.
```thinbasic
TYPE Point2D
  x AS SINGLE
  y AS SINGLE
END TYPE

TYPE Point3D
  x AS SINGLE
  y AS SINGLE
  z AS SINGLE
END TYPE

dim a as Point2D
a.x = 1

dim b as Point3D
b.x = 2

a = b

MSGBOX 0, a.x
MSGBOX 0, b.x
```

> **DANGER:** - allows you to miss the accidental assignment of incompatible data types.

## Arrays in UDT

The following functions do not work with UDT arrays yet:
- `ARRAY ASSIGN`, [reported](https://www.thinbasic.com/community/project.php?issueid=565)
- `ARRAY EXTRACT`, [reported](https://www.thinbasic.com/community/project.php?issueid=566)
- `ARRAY FILL`, [reported](https://www.thinbasic.com/community/project.php?issueid=567)
- `ARRAY SCAN`, [reported](https://www.thinbasic.com/community/project.php?issueid=568)
- `ARRAY SORT`, [reported](https://www.thinbasic.com/community/project.php?issueid=569)
- `ARRAY SUM`, [reported](https://www.thinbasic.com/community/project.php?issueid=570)
- `ARRAY SHIFT`, [reported](https://www.thinbasic.com/community/project.php?issueid=571)
- `ARRAY SHUFFLE`, [reported](https://www.thinbasic.com/community/project.php?issueid=572)
- `ARRAY UNIQUE`, [reported](https://www.thinbasic.com/community/project.php?issueid=573)
- `JOIN$`, [reported](https://www.thinbasic.com/community/project.php?issueid=575)

You can **workaround** these limitations by overlaying virtual array over the UDT array.

Example:
```thinbasic
TYPE MyType
  myArray() as int32
  
  function _Create()
    redim me.myArray(3)
    me.myArray(1) = 1, 2, 3
    
    ' This overlays local array over ME array,
    ' making ME.myArray data available for read/write
    int32 virtualMyArray(3) at varptr(me.myArray(1))
    
    int32 index = array scan virtualMyArray(), = 3
    
    msgbox 0, index
    
  end function
END TYPE

dim v as MyType
```

- `COUNTOF` does not work, [reported](https://www.thinbasic.com/community/project.php?issueid=576)
  - you can workaround by using UBOUND instead

## Multidimensional dynamic arrays in UDT

While static multidimensional arrays in UDT are fully supported with up to 3 dimensions, the dynamic UDT arrays currently work only with a single dimension.

If you dimension dynamic UDT array with more than 1 dimension, it will silently continue, but the indexing will not work correctly.

> **DANGER:** - missing functionality silently ignored, [reported](https://www.thinbasic.com/community/project.php?issueid=563)

You can **workaround** this limitation by overlaying virtual array over the UDT array.

Example:
```thinbasic
TYPE MyType
  myArray() as int32
  
  function _Create()
    redim me.myArray(3 * 2)                             ' -- Linear dimensioning
    
    int32 virtualMyArray(3, 2) at varptr(me.myArray(1)) ' -- Multidimensioning
    
    virtualMyArray(3, 1) = 1    ' Performs write to UDT data thanks to overlay
    virtualMyArray(1, 3) = 2    ' Performs write to UDT data thanks to overlay
    
    msgbox 0, virtualMyArray(3, 1)
    msgbox 0, virtualMyArray(1, 3)    
    
  end function
END TYPE

dim v as MyType
```
