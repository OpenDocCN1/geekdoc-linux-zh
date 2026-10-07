# Chapter 6 · Objects and Classes

The net result is a static inner class is really just a top-level class with a modified naming scheme. In fact, you can use static inner classes as an extension to packaging.

Not only can you declare a class inside another class, but you can also declare a class inside a method of another class. We will discuss this next.

# Classes Defined inside Methods

In the opening of this chapter, we said that nested classes can be declared in any block that this means you can define a class inside a method. This is superbly similar to what you have already seen, but in this case there are three particular points to be considered. The first point is that anything declared inside a method is not a member of the class and is local to the method. The immediate consequence is that classes declared private to the method and cannot be accessed with any access modifier; neither they can be marked as static If you think about this, you'll recognize that these are just the same rules as any variable declaration you make in a method. The second point is that an object created from an inner class within a method can have some access to the variables of the enclosing class. We'll look at how this is done and the restrictions that apply to this in a moment.

Finally, it is possible to create an anonymous class—literally, a class with no specified name—and doing so can be elegant when working with event listeners. We will discuss this technique after the rules governing access from an inner class to method variables in enclosing blocks.

# Accessing Member Variables

The rule that governs the variables of an inner class is simple. Any variable, either a local variable or a formal parameter, can be accessed by methods within an inner class, provided that is marked final. A final is effectively a constant, so the point is simple: an object created inside a method is likely to outlive the method invocation. Local variables and arguments are eventually destroyed when their method exits, these variables would be invalid for any inner methods after the enclosing method exits. Access is only to final variables, it becomes possible to copy the values of those variables into the object, extending their lifetimes. The other possible approach would be writing to two copies of the same data every time it was changed or using local variables onto the heap instead of the stack. Either of these approaches would significantly degrade performance.

Let's look at an example:

+   1. public class Outer {
2. private int m = (int)(Math.random() * 100);
3. public static void main(String args[]) {
4. Outer outer = new Outer();
5. outer.go((int)(Math.random() * 100);
6. (int)(Math.random() * 100));