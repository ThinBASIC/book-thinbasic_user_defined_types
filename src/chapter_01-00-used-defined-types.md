# User defined types

ThinBASIC offers various elemental numeric and string data types. These are very useful in number crunching and text manipulation.

Once you start describing real world objects or more complex math problems, you may feel the need to somehow group the data together into more complex structures.

These structures are called *user defined types* (UDT) in thinBasic.

## Syntax
ThinBASIC uses *type / end type* block to denote *user defined type* definition.
```thinbasic
TYPE nameOfType [alignmentModifier] [EXTENDS baseType]
  element
  [otherElements]
  [dataHandlingfunctions]
END TYPE
```

## Example
The definition of *type* looks complicated, but keep in mind only two parameters are mandatory:
- name of type
- at least one element

To give specific example, if you want to represent a point in 2D, you could design the following UDT:
```thinbasic
TYPE Point2D
  x AS SINGLE
  y AS SINGLE  
END TYPE
```

The name of type is `Point2D` and it has two elements - `x` and `y`, each of `SINGLE` basic data type.  

You can create variable of user defined type the same way as you do with conventional data types:
```thinbasic
DIM point AS Point2D
```

In order to write or read the data, you can use the dot notation:
```thinbasic
point.x = 1
point.y = 2

msgBox 0, strFormat$("{1}, {2}", point.x, point.y) 
```

Arrays of user defined types are supported as well.
