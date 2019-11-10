## Extension

ThinBASIC offers the *extends* keyword to create new UDT by extending existing UDT.

In our case, creating `Point3D` would be as straightforward as:
```thinbasic
TYPE Point3D EXTENDS Point2D
  z AS SINGLE
END TYPE
```

Now, the Point3D will have new `z` element, while the `x` and `y` will be inherited from `Point2D`.

> **Note:** The elements of base UDT will be placed as first in the newly created UDT

> **Note:** In case you would add a new element to base UDT, it will get promoted to UDT which extends it.

> **Note:** In case you would reorder the elements in base UDT, they will get reordered in UDT which extends it.
