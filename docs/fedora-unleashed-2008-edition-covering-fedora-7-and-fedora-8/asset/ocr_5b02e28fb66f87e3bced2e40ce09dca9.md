That demonstrates how the `return` statement sends a value back to the caller, but also how a function can do one thing with lists and another thing with strings. The magic here is being accomplished by the objects. You can write a function that tells two objects to add themselves together, and the objects intrinsically know how to do that. If they don’t—if, perhaps, the user passes in a string and an integer—Python catches the error for you. However, it is this hands-off, “let the objects sort themselves out” attitude that makes functions so flexible. The `concat()` function could conceivably concatenate strings, lists, or *zorks*—a data type someone created herself that allows addition. The point is that you do not limit what your function can do—cliché as it might sound, the only limit is your imagination!

# # Object Orientation

After having read this far, you should not be surprised to hear that Python’s object orientation is flexible and likely to surprise you if you have been using C-like languages for several years.

The best way to learn Python OOP is to just do it. So, here is a basic script that defines a class, creates an object of that class, and calls a function:

```
```
class dog(object):
    def bark(self):
        print "Woof!"

fluffy = dog()
fluffy.bark()
```
```

Defining a class starts, predictably, with the `class` keyword, followed by the name of the class you are defining and a colon. The contents of that class need to be indented one level so that Python knows where each class stops. Note that the `object` inside parentheses is there for object inheritance, which is discussed later. For now, the least you need to know is that if your new class is not based on an existing class, you should put `object` inside parentheses as shown in the previous code.

Functions inside classes work in much the same way as normal functions do (although they are usually called *methods*), with the main difference being that they should all take at least one parameter, usually called `self`. This parameter is filled with the name of the object on which the function was called, and you need to use it explicitly.

Creating an instance of a class is done by assignment. You do not need any `new` keyword, as in some other languages—you just provide empty parentheses. You call a function of