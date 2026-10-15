# OBJECT-ORIENTED CONCEPTS

Visual Basic .NET provides a fully object-oriented environment, which means it bases its functionality around sets of objects. Many languages, such as C++, C#, Java, and others are considered object-oriented as well, and offer many of the same features. You can use object-oriented programming (OOP) to create code you can easily reuse and extend.

Visual Basic versions 6.0 and earlier offered partial implementations of OOP, but VB .NET is the first version of Visual Basic primarily designed around objects.

# CLASS

A class, which contains a set of data, is the primary building block of an object-oriented application. Instead of manipulating data directly as you might in a non-object-oriented language, the class controls how you can access that data from the outside. You can think of a class as having two distinct parts, the interface and the implementation, that provide the ease of use and reusability that are key to development in an OOP language. For more information on classes, see Chapter 7.

In many ways, a class attempts to mimic the way you define things in the real world. For example, you may want to create a program where a ball bounces on the screen. You can place all of the code to define the shape, size, and actions of the ball together with the code to draw and manipulate the user interface. But in an object-oriented language, it makes more sense to create a class to represent the ball.

# OBJECTS

An object is the actual representation you create from your class. A class provides the code and definition that makes up an object. When you create an object, you create a usable version of the class that stores independently in memory. Then you can access the parts of the object, set properties, and work with the abilities its methods provide. You can create any number of objects based on the information from a class. No matter the number of objects you define from a single class, all of the properties and data associated with that object are unique to the individual object.

For example, in your application, assume you want to create a bouncing ball on screen. You define a class that represents a ball. You then create a single instance of the ball in your application, set attributes of the ball, and tell it to bounce. The ball bounces appropriately on screen. You can easily go back to your code for the application, not touching the class defined for the ball, and create a new instance of the class. This ball bounces independently, knowing nothing about the existence of the other balls.

# INTERFACE

The interface of the class provides a way for other parts of the application to access an object. When you define the class, you determine what needs users have for the class and create an interface of properties, methods, and events to make the class usable. When you or someone else creates an object using the class, you do not need to understand its internal functionality. The class internalizes all of its functionality and allows interaction.