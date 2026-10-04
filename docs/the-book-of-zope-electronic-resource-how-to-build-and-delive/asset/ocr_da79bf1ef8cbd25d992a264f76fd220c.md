# Listing 13-3: The sleep() and wakeUp() methods for the Animal class

```
def sleep(self):
    The animal is sleeping
    self.awake=0
    print 'ZZZZZ'
defakeUp(self):
    The animal is awake
    self.awake=1
```

At this point, we can't do very much with the Animal class except to create Animal objects that have a name and a gender and are either awake or sleep-ing. This is simply not a detailed enough description of the real animal world.

# 13.5.1 Creating Subclasses

To better represent the real animal world, we must create additional classes, known as subclasses, of the Animal class. These subclasses assume all the attributes of the Animal class (including name, gender, awake, __init__, sleep, and wakeup) through *inheritance*, and can add their own attributes.

Subclasses inherit the attributes of their base class and expand upon them. Instances of different subclasses share particular attributes they inherit from the same base class.

Let's create two subclasses as an example: the Reptile class and the Bird class. Objects in both classes inherit the same basic attributes from the Animal class and will also have other, new attributes, such as fly and swim.

Subclasses are defined like base classes except that the name of the base class appears in parentheses after the class description.

The Reptile class is defined as shown in Listing 13-4.

# Listing 13-4: The Reptile class: a subclass of the Animal class

```
class reptile(animal):
    ""Reptiles""
    def swim(self):
        ""The reptile swims""
        if self.awake:
            print 'paddle paddle splish splash'
```

The Bird class is defined as shown in Listing 13-5.