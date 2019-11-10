### \_create

The optional `_create` function can be used for variable initialization.

The behaviour slightly differs depending on whether the function has parameters or not.

> **Note:** This function _cannot_ be called explicitly by name, it is used automatically.

#### Without parameters
The simplest form of `_create` does not take any parameters.

Such function is called automatically in case of:
- declaration of a scalar variable of a given type

The typical use of `_create` without parameters is an assignment of the default element values:
```thinbasic
TYPE PacMan
    R AS BYTE
    G AS BYTE
    B AS BYTE

    ' As we all now, PacMan is yellow by default :P
    FUNCTION _create()
        me.R = 255
        me.G = 255
        me.B = 0
    END FUNCTION
END TYPE

DIM player1 AS PacMan   ' player1 is yellow by default

DIM player2 AS PacMan   ' player2 is created yellow by default
player2.R = 0           ' ...but changed to green thanks to override below
player2.G = 255
player2.B = 0
```

> **Note:** Should you create an array of given type, `_create` is not called at the moment.

#### With parameters
The advanced form of `_create` allows us advanced initialization.

For our case of `Point2D` it allows us to set `x` and `y` during the variable creation.

```thinbasic
TYPE Point2D
  x AS SINGLE
  y AS SINGLE
  
  FUNCTION _create(x AS SINGLE, y AS SINGLE)
    ME.x = x
    ME.y = y
  END FUNCTION
END TYPE

DIM point AS Point2D(1, 2)
```

Now `x` contains `1` and `y` is equal to `2`.

As you can see, the `_create` function is not explicitly called, but any parameters passed to your UDT upon creation are passed to `_create` automatically.

Without `_create`, you would need to initialize the variable the hard way:
```
DIM point AS Point2D
point.x = 1
point.y = 2
```

> **Note:** It is still possible to declare `Point2D` as `DIM point AS Point2D`, without any parameters. In such a case `_create` is not called and `x` and `y` will both have a value of zero.
