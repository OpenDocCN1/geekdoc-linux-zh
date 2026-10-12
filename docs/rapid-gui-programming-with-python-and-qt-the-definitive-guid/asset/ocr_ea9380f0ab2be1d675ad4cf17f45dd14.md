must put self as the first item of every (nonstatic*) method’s parameter list, although we never need to pass it since Python will do that for us.

Although the name “self” is merely conventional, we will always use it. Inside the object, we must use self explicitly when we want to refer to instance methods or attributes. For example, in the Chair class’s initializer, we have created two data attributes using self. Thanks to Python’s dynamic nature, it is possible to create additional attributes in other methods, and even to add additional attributes to particular instances if we wish; but we will take a more conservative line that is sufficient for the GUI programming we are working toward.

To create an instance of a class, we use the following syntax:

```
instance = className(arguments)
```

The parentheses are mandatory, even if we don’t pass any arguments. Behind the scenes, Python constructs the object by calling the class’s static `__new__()` method (which is inherited from object, or in rare cases is implemented by us), and then calls `__init__()` on the newly constructed object. The resulting initialized object is returned.

In the case of our Chair class, we must pass either one or two arguments (Python passes the first self argument automatically for us); for example:

```
chair1 = Chair("Barcelona")
chair2 = Chair("Bar Stool", 1)
```

Since the attributes are public, they can be read or assigned to using the dot (.) operator; for example: print chair2.name will print “Bar Stool”, and chair1.legs = 2 will change chair1’s legs attribute’s value from 4 to 2.

Object-oriented purists may no doubt be uncomfortable with this kind of direct access to attributes from outside the instance, whereas those with a taste for extreme programming may be perfectly happy with it since we can always add accessor methods later.

Now that we have seen how construction and initialization are handled, we need to consider object destruction. C++ programmers are used to using destructors and relying on the fact that they can delete objects at a time of their own choosing. Java and Python programmers do not have that particular luxury. Instead, they have automatic garbage collection, which makes programming much easier in general but with one drawback of not giving fine control over exactly when objects are deleted. If resources need to be protected, the solution is normally to use a try ... finally block to guarantee cleanup. When an object is about to be garbage-collected its `__del__()` special method is called, with self as its only argument. As is common practice in Python (and in Java regarding the finalize() method), we very rarely use this particular special