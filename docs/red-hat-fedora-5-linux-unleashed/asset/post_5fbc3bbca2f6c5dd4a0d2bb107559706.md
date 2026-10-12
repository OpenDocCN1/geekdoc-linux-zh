
## Functions

Other languages—such as PHP—read and process an entire file before executing it, which means you can call a function before it is defined because the compiler will read the definition of the function before it tries to call it. Python is different: If the function definition has not been reached by the time you try to call it, you get an error. The reason behind this behavior is that Python actually creates an object for your function, and that in turn means two things. First, you can define the same function several times in a script and have the script pick the right one at runtime. Second, you can assign the function to another name just by using `=`.

A function definition starts with `def`, followed by the function name, parentheses and a list of parameters, and then a colon. The contents of a function need to be indented at least one level beyond the definition. So, using function assignment and dynamic declaration, you can write a script that prints the right greeting in a roundabout manner:

```python
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
Hello, Paul!
```

Notice that function definitions include no type information. Functions are typeless, as we said. The upside of this is that you can write one function to do several things:

```python
>>> def concat(First, Second):
...     return First + Second
>>> concat(["python"], ["perl"])
['python', 'perl']
>>> concat("Hello, ", "world!")
'Hello, world!'
```

That demonstrates how the `return` statement sends a value back to the caller, but also how a function can do one thing with lists and another thing with strings. The magic here is being accomplished by the objects. We wrote a function that tells two objects to add themselves together, and the objects intrinsically know how to do that. If they don't—if, perhaps, the user passes in a string and an integer—Python catches the error for us. However, it is this hands-off, "let the objects sort themselves out" attitude that makes functions so flexible. Our `concat()` function could conceivably concatenate strings, lists, or zorks—a data type someone created herself that allows adding. The point is that we do not limit what our function can do—cliché as it might sound, the only limit is your imagination!

## Object Orientation

After having read this far, you should not be surprised to hear that Python's object orientation is flexible and likely to surprise you if you have been using C-like languages for several years.

The best way to learn Python OOP is to just do it. So, here is a basic script that defines a class, creates an object of that class, and calls a function:

```python
class dog(object):
    def bark(self):
        print "Woof!"

fluffy = dog()
fluffy.bark()
```

Defining a class starts, predictably, with the `class` keyword followed by the name of the class you are defining and a colon. The contents of that class need to be indented one level so that Python knows where it stops. Note that the `object` inside parentheses is there for object inheritance, which is discussed later. For now, the least you need to know is that if your new class is not based on an existing class, you should put `object` inside parentheses as shown in the previous code.

Functions inside classes work in much the same way as normal functions do (although they are usually called methods), with the main difference being that they should all take at least one parameter, usually called `self`. This parameter is filled with the name of the object the function was called on, and you need to use it explicitly.

Creating an instance of a class is done by assignment. You do not need any new keyword, as in some other languages—you just provide empty parentheses. Calling a function of that object is done using a period, the name of the class to call, with any parameters being passed inside parentheses.

## Class and Object Variables

Each object has its own set of functions and variables, and you can manipulate those variables independent of objects of the same type. Additionally, some class variables are set to a default value for all classes and can also be manipulated globally.

This script demonstrates two objects of the `dog` class being created, each with its own name:

```python
class dog(object):
    name = "Lassie"
    def bark(self):
        print self.name + ' says "Woof!"'
    def setName(self, name):
        self.name = name

fluffy = dog()
fluffy.bark()

poppy = dog()
poppy.setName('Poppy')
poppy.bark()
```

That outputs the following:

```
Lassie says "Woof!"
Poppy says "Woof!"
```

Each dog starts with the name Lassie, but it gets customized. Keep in mind that Python assigns by reference by default, meaning each object has a reference to the class's name variable, and as we assign that with the `setName()` method, that reference is lost. What this means is that any references we do not change can be manipulated globally. Thus, if we change a class's variable, it also changes in all instances of that class that have not set their own value for that variable. For example:

```python
class dog(object):
    name = "Lassie"
    color = "brown"

fluffy = dog()
poppy = dog()
print fluffy.color
dog.color = "black"
print poppy.color
poppy.color = 'yellow'
print fluffy.color
print poppy.color
```

So, the default color of dogs is brown—both the fluffy and poppy dog objects start off as brown. Then, using `dog.color`, we set the default color to be black, and because neither of the two objects has set its own color value, they are updated to be black. The third to last line uses `poppy.color` to set a custom color value for the poppy object—poppy becomes yellow, but fluffy and the dog class in general remain black.

### Constructors and Destructors

To help you automate the creation and deletion of objects, you can easily override two default methods: `__init__` and `__del__`. These are the methods called by Python when a class is being instantiated and freed, known as the constructor and destructor, respectively.

Having a custom constructor is great when you need to accept a set of parameters for each object being created. For example, you might want each dog to have its own name on creation, and you could implement that with this code:

```python
class dog(object):
 def __init__(self, name):
  self.name = name
fluffy = dog("Fluffy")
print fluffy.name
```

If you do not provide a name parameter when creating the dog object, Python reports an error and stops. You can, of course, ask for as many constructor parameters as you want, although it is usually better to ask for only the ones you need and have other functions to fill in the rest.

On the other side of things is the destructor method, which allows you to have more control over what happens when an object is destroyed. Using the two, we can show the life cycle of an object by printing messages when it is created and deleted:

```python
class dog(object):
 def __init__(self, name):
  self.name = name
  print self.name + " is alive!"

 def __del__(self):
  print self.name + " is no more!"
fluffy = dog("Fluffy")
```

The destructor is there to give you the chance to free up resources allocated to the object or perhaps log something to a file.

### Class Inheritance

Python allows you to reuse your code by inheriting one class from one or more others. For example, lions, tigers, and bears are all mammals and so share a number of similar properties. In that scenario, you would not want to have to copy and paste functions between them; it would be smarter (and easier!) to have a `mammal` class that defines all the shared functionality and then inherit each animal from that.

Consider the following code:

```python
class car(object):
    color = 'black'
    speed = 0

    def accelerateTo(self, speed):
        self.speed = speed

    def setColor(self, color):
        self.color = color

mycar = car()
print mycar.color
```

This creates a `car` class with a default color and also provides a `setColor()` function so that people can change their own colors. Now, what do you drive to work? Is it a car? Sure it is, but chances are it is a Ford, or a Dodge, or a Jeep, or some other make—you don't get cars without a make. On the other hand, you do not want to have to define a class `ford`, give it the methods `accelerateTo()`, `setColor()`, and however many other methods a basic `car` has and then do exactly the same thing for Ferrari, Nissan, and so on?

The solution is to use inheritance: Define a `car` class that contains all the shared functions and variables of all the makes and then inherit from that. In Python, you do this by putting the name of the class from which to inherit inside parentheses in the class declaration, like this:

```python
class car(object):
    color = 'black'
    speed = 0

    def accelerateTo(self, speed):
        self.speed = speed

    def setColor(self, color):
        self.color = color

class ford(car): pass
class nissan(car): pass
mycar = ford()
print mycar.color
```
