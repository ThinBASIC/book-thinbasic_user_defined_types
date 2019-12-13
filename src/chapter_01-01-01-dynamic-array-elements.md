## Dynamic array elements

There is one single exception when UDT array does not have to be dimensioned at all. We call such arrays _dynamic_ and their usage is strictly restricted to use in conjunction with [UDT functions](chapter_01-04-02-udt-function.html), which can (re)dimension them before first use.

```
TYPE Person
  firstName      AS STRING
  secondName     AS STRING

  luckyNumbers() AS LONG

  ...

END TYPE
```

Dynamic array element has then just empty brackets specified, to distinguish it from a simple element.

> **Limitation:** You cannot create dynamic arrays of UDTs at the moment, only elemental numeric and string types can be used
