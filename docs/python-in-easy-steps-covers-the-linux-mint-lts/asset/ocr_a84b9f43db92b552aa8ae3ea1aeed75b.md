Typically, instance variables contain data passed by the caller when an instance copy of the class is created. As this data is only available locally for internal use, it is effectively hidden from the rest of the program. This technique of data "encapsulation" ensures that data is securely stored within the class structure and is the first principle of Object Oriented Programming (OOP).

![](bbox=[0.12, 0.22, 0.23, 0.31])

It is conventional to begin class names with an uppercase character, and object names with lowercase.

All properties of a class are referenced internally by the dot notation prefix self – so an attribute named “sound” is self.sound. Additionally, all method definitions in a class must have self as their first argument – so a method named “talk” is talk( self ).

When a class instance is created, a special __init__ ( self ) method is automatically called. Subsequent arguments can be added in its parentheses if values are to be passed to initialize its attributes.

A complete Python class declaration could look like this example:

```
class Critter:
    "" A base class for all critter properties. ""
    count = 0

    def __init__( self , chat ):
        self.sound = chat
        Critter.count += 1

    def talk ( self ):
        return self.sound
```

It is useful to examine the class components of this example:

+   - The variable count is a class variable whose integer value gets shared among all instances of this class – this value can be referenced as Critter.count from inside or outside the class.