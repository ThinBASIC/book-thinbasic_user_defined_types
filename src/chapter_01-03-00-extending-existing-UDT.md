# Extending existing UDT

Once designing a new type, you don't have to start from scratch.

Imagine our `Point2D` type, defined in the previous chapters.

It has two members, `x` and `y`.
```thinbasic
TYPE Point2D
  x AS SINGLE
  y AS SINGLE
END TYPE
```

Once you will need to create 3D point, the obvious approach would be to do it this way:
```thinbasic
TYPE Point3D
  x AS SINGLE
  y AS SINGLE
  z AS SINGLE
END TYPE
```

The advantage of this copy-paste approach is that it is straightforward, but once you would add something to `Point2D`, it would need to be promoted to `Point3D` manually.

Let's have a look at two different approaches creating new type based on an existing one.
