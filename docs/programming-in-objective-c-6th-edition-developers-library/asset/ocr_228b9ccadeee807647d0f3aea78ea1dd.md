The actions listed in **Table 18.1** can be done with your car, and they can also be done with other cars. For example, your sister can drive her car, wash it, fill it up with gas, and so on.

# ### Instances and Methods

A unique occurrence of a class is an instance. The actions that you perform are called *methods*. In some cases, a method can be applied to an instance of the class or to the class itself. For example, washing your car applies to an instance (in fact, all of the methods listed in **Table 18.1** are considered instance methods). Finding out how many different types of cars a manufacturer makes applies to the class, so it is a class method.

In C++, you invoke a method on an instance using the following notation:

```
```
Instance.method
```
```

A C# method is invoked with the same notation as follows:

```
```
Instance.method
```
```

An Objective-C message call follows this format:

```
```
[Instance  method]
```
```

Go back to the previous list and write a message expression in this new syntax. Assume that Y is an object from the C class. **Table 18.2** shows what message expressions might look like in the three OOP languages.

Table 18.2 Message Expressions in OOP Languages

And if your sister has a car, called s, for example, then she can invoke the same methods on her car, as follows:

![](bbox=[0.01, 0.75, 0.29, 0.76])

```
```
s.
```

```

This is one of the key concepts behind object-oriented programming (that is, applying the same methods to different objects).

Another key concept, known as polymorphism, allows you to send the same message to instances from different classes. For example, if you have a B class, and an instance from that class called m, then polymorphism allows you to write the following message expressions in C++:

```
```
m
m
```

```

The key here is that you can write a method for the B class that knows about servicing a boat, that can be (and probably is) completely different from the method in the C class that knows how to