## Simple elements
```thinbasic
elementName AS elementType 
```

Element definition has two mandatory parts:
- *elementName*, following the same naming rules as any other variable
- *elementType*, which can be any numeric, string or user defined type

An example of UDT with simple elements follows:
```thinbasic
TYPE Point2D
  x AS SINGLE
  y AS SINGLE  
END TYPE
```

Each element is specified on a new line.
