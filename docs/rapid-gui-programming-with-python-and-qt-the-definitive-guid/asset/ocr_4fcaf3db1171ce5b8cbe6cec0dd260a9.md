Now that we can encapsulate some basic information about a work of art, we can create a Painting subclass to hold information on paintings:

```
class Painting(Item):
    def __init__(self, artist, title, year=None):
        super(Painting, self).__init__(artist, title, year)
```

The preceding code is the entire subclass. We have not added any data attributes or new methods, so we just use the `super()` built-in function to initialize the `Item` base class. The `super()` function takes a class and returns the class’s base class. If the function is also passed an instance (as we do here), the returned base class object is bound to the instance we passed in, which means we can call (base class) methods on the instance.

It is also possible to call the base class by naming it explicitly—for example, `Item.__init__(self, artist, title, year)`; notice that we must pass the `self` parameter ourselves if we use this approach.

We don’t have to call the base class `__init__()` at all—for example, if the base class has no data attributes. And if we do call it, the `super()` call does not have to be the first call we make, although it usually is in `__init__()` implementations.

Now we will look at a slightly more elaborate subclass:

```
class Sculpture(Item):
    def __init__(self, artist, title, year=None, material=None):
        super(Sculpture, self).__init__(artist, title, year)
        self._material = material
```

The `Sculpture` class has an additional attribute, so after initializing through the base class we also initialize the extra attribute.

We won’t show the accessors since they are structurally the same as those used for the artist’s name.

```
def __str__(self):
    materialString = ""
    if self._material is not None:
        materialString = " (%s)" % self._material
    return "%%s%%s" % (super(Sculpture, self).__str__(), materialString)
```

The `__str__()` method uses the base class’s `__str__()` method, and if the material is known, it tacks it on to the end of the resultant string. We cannot call `str(self)` because that would lead to an infinite recursion (calling `__str__()` again and again), but there is no problem calling a special method explicitly when necessary, as we do here.