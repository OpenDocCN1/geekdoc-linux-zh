# Implementing Object-Oriented Relationships

This section considers the implementation of classes for which you have been given a basic description.
There are two phrases that are commonly used when describing a class in plain English: “is a” and “has a.”. As a working simplification, they are used to describe the superclass and member variables, respectively. For example, consider this description:
“A home is a house that has a family and a pet.”
This description would give to the outline of a Java class in this form:

+   1. public class Home extends House {
2. Family inhabitants;
3. Pet getPet;
4. )

Notice the direct correspondence between the “is a” clause and the extends clause. In this example, a direct correspondence also exists between the items listed after “has a” and the variables. Such a correspondence is representative of simple examples and in a test situation; however, you should be aware that in real examples, there are other ways to provide a class with attributes. The most important of these alternatives is the approach taken by JavaBeans, which is to supply accessor and mutator methods that operate on data members.

![](bbox=[0.168, 0.566, 0.248, 0.626])

The example shown is simplified to focus on the knowledge and understanding that is required by the exam. In a real situation, the variables should generally be private (or at least some specific rationale should apply to whatever accessibility they have), and some methods will be needed in the class.

# Methods, Overloading and Overriding

As you construct classes and add methods to them, in some circumstances you will want to re-use the same name for a method. You can do so two ways with Java. Using the same method with different arguments and perhaps a different return type is known as overloading. A method can be re-used anywhere, as long as certain conditions are:

+   * In an unrelated class, no special conditions apply, and the two methods are not considered related in any way.
* In the class that defines the original method, or a subclass of that class, the method name can be re-used if the argument list differs in terms of the type of at least one argument. This