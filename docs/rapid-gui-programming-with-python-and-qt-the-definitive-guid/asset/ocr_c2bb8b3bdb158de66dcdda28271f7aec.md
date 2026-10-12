```
```
def partial(func, arg):
    def callme():
        return func(arg)
    return callme
```
```

Inside the partial() function we create an inner function, callme(), that, when called, will call the function and argument that were passed to the partial() function. After creating the callme() function, we then return an object reference to it so that it can be called later.

This means that we can now write:

```
```
buttonOneFunc = partial(action, "One")
buttonTwoFunc = partial(action, "Two")
```
```

Ideally, it would be nice to use functools.partial() when it is available, and fall back on our own simple partial() function otherwise. Well, since we can define functions at runtime, this is perfectly possible:

```
```
import sys

if sys.version_info[:2] < (2, 5):
    def partial(func, arg):
        def callme():
            return func(arg)
        return callme
else:
    from functools import partial
```
```

The if statement ensures that if we are using a version of Python older than 2.5 we create a partial() function that takes a function and a single argument and returns a function that, when called, will call the function passed in with the argument. But if we are using a later version of Python, we use the functools.partial() function, so in our code we can always call partial(), and whichever version was created will be the one used.

Now, just as before, we can write:

```
```
buttonOneFunc = partial(action, "One")
buttonTwoFunc = partial(action, "Two")
```
```

Only this time the code will work with both old and new versions of Python. The partial() function we have defined is just about the simplest possible. It is also possible to create much more sophisticated wrappers that can take positional and keyword arguments at the time they are wrapped, and additional positional and keyword arguments at the time they are called; functionality that functools.partial() already provides. We use partial() in several places from Part II onward, but in each case the simple partial() function shown in this section could be used if Python 2.5 or later was not available.