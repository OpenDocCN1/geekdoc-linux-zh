Here we return the result of comparing the heights if the widths are the same; otherwise, we return the result of comparing the widths.

If we do not reimplement any comparison special methods, in most cases Python will happily perform comparisons for us, although not necessarily in the way we would want. If we are creating a class where comparisons make sense, we ought to implement \_\_cmp\_\_(). For other classes, the safest thing to do is to implement \_\_cmp\_\_() with a body of return NotImplemented error.

```
```
def __nonzero__ (self):
    return self.width or self.height
```
```

This special method is used when the object is in a Boolean context; for example, bool(rectA), or if rectB: and returns True if the object is “nonzero”.

```
```
def __repr__ (self):
    return "Rectangle(%d, %d)" % (self.width, self.height)
```
```

The “representation” special method must return a string which, if evaluated (e.g., using eval()), will result in the construction of an object with the same properties as the object it is called on. Some objects are too complex to support this, and for some objects, such as a window or a button in a GUI, it doesn’t make sense; so such classes don’t provide a \_\_repr\_\_() implementation. In a string% operator’s format string we use \*r to get the result of this special method; we can also use the repr() function or the backticks \*\*\* operator. Backticks are just a syntactic alternative to using repr(). For example, repr(x) and \*x\* both return identical results: the representation of object x as returned by x’s \_\_repr\_\_() method.

There is also a \_\_str\_\_() special method that must return a string representation of the object it is called on (like Java’s toString() method), but unlike \_\_repr\_\_(), the representation is meant to be human-readable and does not have to be eval()-able. If, as in this case, the \_\_str\_\_() method is not implemented, Python will use the \_\_repr\_\_() method instead. For example:

```
```
rect = Rectangle(8, 9)
print rect    # Prints "Rectangle(8, 9)" using __repr__()
```
```

If we want a human-readable Unicode string representation of our class, we can implement \_\_unicode\_\_().

There are a few more general special methods that we could implement, but which are not appropriate for the Rectangle class. All the commonly implemented general special methods are listed in Table 3.1.