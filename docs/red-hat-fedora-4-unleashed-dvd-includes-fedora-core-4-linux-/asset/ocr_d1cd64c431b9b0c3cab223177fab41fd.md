# ## Class Inheritance

Python allows you to reuse your code by inheriting one class from one or more others. For example, lions, tigers, and bears are all mammals and so share a number of similar properties. In that scenario, you would not want to have to copy and paste functions between them; it would be smarter (and easier!) to have a mammal class that defines all the shared functionality and then inherit each animal from that.

Consider the following code:

```
```
class car(object):
    color = "black"
    speed = 0

    def accelerateTo(self, speed):
        self.speed = speed

    def setColor(self, color):
        self.color = color

mycar = car()
print mycar.color
```
```

That creates a car class with a default color and also provides a setColor() function so people can change their own colors. Now, what do you drive to work? Is it a car? Sure it is, but chances are it is a Ford, or a Dodge, or a Jeep, or some other make—you don't get cars without a make. On the other hand, you do not want to have to define a class Ford, give it the methods accelerateTo(), setColor(), and however many other methods a basic car has and then do exactly the same thing for Ferrari, Nissan, and so on.

The solution is to use inheritance: Define a car class that contains all the shared functions and variables of all the makes and then inherit from that. In Python, you do this by putting the name of the class from which to inherit inside parentheses in the class declaration, like this:

```
```
class car(object):
    color = "black"
    speed = 0

    def accelerateTo(self, speed):
        self.speed = speed

    def setColor(self, color):
        self.color = color
```
```

```
```
class ford(car): pass
class nissan(car): pass
mycar = ford()
print mycar.color
```
```

The pass directive is an empty statement—it means our class contains nothing new. However, because the ford and nissan classes inherit from the car class, they get color, speed, accelerateTo(), and setColor() provided by their parent class. Note that we do