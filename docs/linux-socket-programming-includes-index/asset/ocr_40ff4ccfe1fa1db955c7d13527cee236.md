# Multiple Inheritance Conundrum

Another complexity stems from the features of inheritance. The C++ language lets you create classes that inherit from multiple parent classes. Managing an inheritance hierarchy is difficult enough. Chapter 11, “Saving Time with Objects,” mentions the concept of coupling. Inheriting from multiple sources introduces unhealthy coupling between classes.

This coupling forms a dependency on the parent classes. If these classes change, the designer has to verify the interfaces between them and the subclass. The changes sometimes are very subtle but may require special name resolutions in the subclass. This is pretty messy.

From a theoretical view, multiple inheritance is viable but impractical. A design that has multiple inheritances is typically broken. Most of the reasons stem from improper responsibility delegation or class naming. The most common cause is improper abstraction and delegation. Often, the two parent classes have a common set of behaviors that should be extracted and placed above them as a superclass.

Another common cause of multiple inheritance is naming a class with a verb. For example, if you have StreamReader and StreamWriter, you must merge the two to get a random access Stream. The names *Reader* and *Writer* are the problem.

You can solve the majority of multiple inheritance problems either by pulling out the common features into an abstract superclass or by using containers. Usually, the new class is more similar to one parent class than to the other. Inherit from the more similar class, and contain the other one.

Task-classes prove to be a small exception to that rule. If you have a class that is related to one parent class and is also a task (process or thread), you may be stuck using multiple inheritance. The reason is that the class cannot contain a task-class: The programming just does not work very well. Your subclass is usually more related to the other class.

To solve the task-class problem without multiple inheritance, you may have to force the subclass to inherit from the task and contain the other class. It’s doable but can be cumbersome.

# Code Bloat

The inheritances, abstractions, overloads, and templates are tremendous helps in getting your job done quickly. However, you can run into another problem: source- and object-code bloat. The increases in object size may not be important if you have plenty of memory. But the more lines of code you write, the more likely the program has defects.

Depending on the complexity of your classes, you can see a 20% to 50% increase in the number of lines of code you have to write compared to a modular design. This is largely due to the language syntax and support. With the sacrifice of increased source complexity, you do get more capability and stronger typing.