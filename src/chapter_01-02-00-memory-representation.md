# Memory representation

This chapter covers an advanced technical topic. Continue reading, if you plan to:
- manipulate UDT variables via pointers
- pass UDT variables to 3rd party DLLs

Otherwise, feel free to continue to the next chapter.

The order in which are members declared is also reflected in the binary representation of the variable in memory.

Let's demonstrate it on our exemplar UDT:
```thinbasic
TYPE Point2D
  x AS SINGLE
  y AS SINGLE
END TYPE
```

In this case, the element `x` is placed in memory first, and element `y` afterwards.

Continue reading to explore how to determine size, element offsets and sizes in memory.
