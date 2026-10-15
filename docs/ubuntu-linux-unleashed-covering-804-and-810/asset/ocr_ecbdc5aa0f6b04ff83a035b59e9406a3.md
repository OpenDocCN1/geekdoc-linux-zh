# ## Class and Object Variables

Each object has its own set of functions and variables, and you can manipulate those variables independently of objects of the same type. In addition, some class variables are set to a default value for all classes and can be manipulated globally.

This script demonstrates two objects of the dog class being created, each with its own name:

```
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
poppy.setName("Poppy")
poppy.bark()
```
```

That outputs the following:

```
```text
Lassie says 'Woof!'
Poppy says 'Woof!'
```
```

There, each dog starts with the name Lassie, but it gets customized. Keep in mind that Python strings by reference by default, meaning each object has a reference to the class's name variable, and as we assign that with the setName() method, that reference is lost. What this means is that any references we do not change can be manipulated globally. Thus, if we change a class's variable, it also changes in all instances of that class that have not set their own value for that variable. For example:

```
```python
class dog(object):
    name = "Lassie"
    color = "brown"
fluffy = dog()
poppy = dog()
print fluffy.color
dog.color = "black"
print poppy.color
fluffy.color = "yellow"
print fluffy.color
print poppy.color
```
```

So, the default color of dogs is brown—both the fluffy and poppy dog objects start off as brown. Then, using dog.color, we set the default color to be black, and because neither of the two objects has set its own color value, they are updated to be black. The third to last line uses poppy.color to set a custom color value for the poppy object—poppy becomes yellow, while fluffy and the dog class in general remain black.