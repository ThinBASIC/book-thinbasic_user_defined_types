### UDT function

You can enhance the UDT with functions as well - this approach is appropriate anytime you need to perform the data manipulation of the UDT itself.

Imagine our `Point2D` example - you will most probably need to initialize `x` and `y` straight away, and you will most probably need to be able to get string representation of the variable.

Let's use this example to demonstrate the use of UDT functions.

The first fact you should now is that UDT functions do not take the UDT variable as input explicitly.

The data is always reachable via pre-defined `ME` variable, accessible in each UDT function.

There are two kinds of UDT functions:
- user defined functions
- functions with special meaning, currently `_create` and `_destroy`

#### User defined function within TYPE definition

You can define a function directly inside the *type / end type* block.

The same rules apply as for any other function, except the advantage of having `ME` as a way to reference UDT elements.

```thinbasic
TYPE Point2D
  x AS SINGLE
  y AS SINGLE
  
  FUNCTION setXY(x AS SINGLE, y AS SINGLE)
    ME.x = x
    ME.y = y
  END FUNCTION
  
  FUNCTION toString() AS STRING
    RETURN strFormat$("[{1}, {2}]", ME.x, ME.y)
  END FUNCTION
END TYPE

DIM point AS Point2D

point.setXY(1, 2)
msgBox point.toString()
``` 

The main advantage of this type of definition is that the *type / end type* contains everything the UDT can do.

#### User defined function outside TYPE definition

You can define the function body outside the *type / end type* block as well.

In such a case, please register the function via `<functionName> AS FUNCTION` within the *type / end type* first. This registration does not increase the memory footprint of the UDT, but it creates logical link between UDT and function.

UDT function defined outside the *type / end type* block follows the same rules as any other function, except:
- having `ME` as a way to reference UDT elements
- need to prefix the function name with name of type and dot

```thinbasic
TYPE Point2D
  x AS SINGLE
  y AS SINGLE

  setXY    AS FUNCTION
  toString AS FUNCTION  
END TYPE

FUNCTION Point2D.setXY(x AS SINGLE, y AS SINGLE)
  ME.x = x
  ME.y = y
END FUNCTION

FUNCTION Point2D.toString() AS STRING
  RETURN strFormat$("[{1}, {2}]", ME.x, ME.y)
END FUNCTION

DIM point AS Point2D

point.setXY(1, 2)
msgBox point.toString()
``` 

The main advantage of this type of definition is that you can spread the function across multiple source code files.
  
#### _create

The optional `_create` function has following properties:
- is automatically called once the variable is defined
- it should never be called explicitly
- it can take parameters, which can be used for initialization

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

As you can see, the `_create` function is not explicitely called, but any parameters passed to your UDT upon creation are passed to `_create` automatically.

Without `_create`, you would need to initialize the variable the hard way:
```
DIM point AS Point2D
point.x = 1
point.y = 2
```

#### _destroy 

The optional `_destroy` function has two basic properties:
- is automatically called once the variable goes out of scope
- it does not take any parameters 

Defining it in context of `Point2D` has no meaning, but we can use it to illustrate how it works:

```
TYPE Point2D
  x AS SINGLE
  y AS SINGLE
  
  FUNCTION _create(x AS SINGLE, y AS SINGLE)
    ME.x = x
    ME.y = y
    msgBox strFormat$("Point2D Variable is being created with x = {1}, y = {2}", ME.x, ME.y)
  END FUNCTION
  
  FUNCTION _destroy()
    msgBox "Point2D Variable is being released"
  END FUNCTION  
END TYPE

msgBox "Hello, I am about to call MyFunction"

MyFunction()

msgBox "Hello, I finished calling MyFunction"

FUNCTION MyFunction()
  DIM p AS Point2D(1, 2)
END FUNCTION
```
