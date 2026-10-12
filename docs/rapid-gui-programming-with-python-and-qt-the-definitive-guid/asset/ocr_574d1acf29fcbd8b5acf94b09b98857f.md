vance, it would be nice to be able to somehow package up both the function to be called and the parameter we want to use into a single callable object.

A solution to this is *partial function application* (also known as "currying"), which simply means that we take a function and zero, one, or more parameters for it, and wrap them up into a new function which, when invoked, will call the original function with the parameters we wrapped, and with any others that are passed at call time. Such wrapped functions are called *closures* because they encapsulate some of their calling context when they are created.

To get a flavor for how this works, let us imagine a very simple GUI program where we have two buttons that, when pressed, will call the same `action()` function. (We won't worry about how we transform button presses into function calls right now; it is very easy, and fully explained in Chapter 4.)

```
def action(button):
    print "You pressed button", button
```

Now when we create our buttons, naturally we know which ones they are, so we want to tell the first button to make the call `action("One")` and the second to call `action("Two")`. But this presents us with a problem. We know what we want called, but we don't want the call to take place until a button is pressed. So, for example, we want to give the first button a function which wraps `action()` and the parameter "One", so that when the first button is pressed it can call `action()` with the right parameter.

So, what we need is a function that will take a function and an argument and return a function, that when, called will call the original function with the original argument. In Python 2.5, this is easy assuming our previous definition of `action()`:

```
import functools

buttonOneFunc = functools.partial(action, "One")
buttonTwoFunc = functools.partial(action, "Two")
```

The `functools.partial()` function takes a function as the first argument, and then any number of other arguments, and returns a function that, when called, will call the passed function with the passed arguments, and with any additional arguments that are given at call time.

So, when `buttonOneFunc()` is called, it will simply call `action("One")` just as we want. As we mentioned earlier, a function's name is simply an object reference that happens to refer to a function, so it can be passed as a parameter like any other object reference.

But where does this leave users of earlier versions of Python? We could provide our own very simple and less powerful version of `partial()`. For example: