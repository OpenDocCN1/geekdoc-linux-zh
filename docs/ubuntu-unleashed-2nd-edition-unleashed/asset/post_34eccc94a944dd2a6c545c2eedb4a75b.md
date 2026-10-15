
You can control loops using the break and continue keywords. break exits the loop and continues processing immediately afterward, and continue jumps to the next loop iteration.

## Functions

Other languages—such as PHP—read and process an entire file before executing it, which means you can call a function before it is defined because the compiler reads the definition of the function before it tries to call it. Python is different: If the function definition has not been reached by the time you try to call it, you get an error. The reason behind this behavior is that Python actually creates an object for your function, and that in turns means two things. First, you can define the same function several times in a script and have the script pick the right one at runtime. Second, you can assign the function to another name just by using =.

Function definition starts with def, then the function name, then parentheses and a list of parameters, and then a colon. The contents of a function need to be indented at least one level beyond the definition. So, using function assignment and dynamic declaration, you can write a script that prints the right greeting in a roundabout manner:

```
>>> def hello_english(Name):
...     print "Hello, " + Name + "!"
...
>>> def hello_hungarian(Name):
...     print "Szia, " + Name + "!"
...
>>> hello = hello_hungarian
>>> hello("Paul")
Szia, Paul!
>>> hello = hello_english
>>> hello("Paul")
```

Notice that function definitions include no type information. Functions are typeless, like we said. The upside of this is that you can write one function to do several things:

```
>>> def concat(First, Second):
...     return First + Second
...
>>> concat(["python"], ["perl"])
['python', 'perl']
```

```
```python
>>> concat("Hello, ", "world!")
'Hello, world!'
```
```

That demonstrates how the return statement sends a value back to the caller, but also how a function can do one thing with lists and another thing with strings. The magic here is being accomplished by the objects. We write a function that tells two objects to add themselves together, and the objects intrinsically know how to do that. If they don’t—if, perhaps, the user passes in a string and an integer—Python catches the error for us. However, it is this hands-off, “let the objects sort themselves out” attitude that makes functions so flexible. Our concat() function could conceivably concatenate strings, lists, or zonks—a data type someone created herself that allows adding. The point is that we do not limit what our function can do—tacky as it might sound, the only limit is your imagination!

## Object Orientation

After having read this far, you should not be surprised to hear that Python’s object orientation is flexible and likely to surprise you if you have been using C-like languages for several years.

The best way to learn Python object-oriented programming (OOP) is to just do it. So, here is a basic script that defines a class, creates an object of that class, and calls a function:

```
```python
class dog(object):
    def bark(self):
        print "Woof!"

fluffy = dog()
fluffy.bark()
```
```

Defining a class starts, predictably, with the class keyword followed by the name of the class you are defining and a colon. The contents of that class need to be indented one level so that Python knows where it stops. Note that the object inside parentheses is there for object inheritance, which is discussed later. For now, the least you need to know is that if your new class is not based on an existing class, you should put object inside parentheses as shown in the previous code.

Functions inside classes work in much the same way as normal functions do (although they are usually called methods), with the main difference being that they should all take at least one parameter, usually called self. This parameter is filled with the name of the object the function was called on, and you need to use it explicitly.

Creating an instance of a class is done by assignment. You do not need any new keyword, as in some other languages—you just provide empty parentheses. Calling a function of that object is done using a period, the name of the class to call, with any parameters being passed inside parentheses.
