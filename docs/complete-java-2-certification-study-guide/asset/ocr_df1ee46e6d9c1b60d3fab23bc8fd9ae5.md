# Chapter 6 · Objects and Classes

a method differ slightly from the more general case of inner classes that are defined as members
of a class; we will look at these differences in detail. For now, when we refer to a "member
class," we mean a class that is not defined in method but rather in a class. In this context,
of of the term member is closely parallel to its use in the context of member variables and mem-
methods.

The complexity of inner classes relates to scope and access—particularly to variables
enclosing scopes. Before we consider these matters, let's look at the syntax of access to basic inner
class, which is really quite simple. Consider this example:

+   1. public class OuterOne {
2.   private int x;
3.   public class InnerOne {
4.   private int y;
5.   public void innerMethod() {
6.     System.out.println("y is " + y);
7.   }
8.   }
9.   public void outerMethod() {
10.    System.out.println("x is " + x);
11.  }
12.  // other methods...
13. }

In this example, there is no obvious benefit in declaring the class InnerOne as an
inner class; so we are only looking at the syntax of the fully qualified name of the inner class. In this,
enclosing class name becomes part of the full name of the inner class. The
two classes "full names are OuterOne and OuterOne.InnerOne." This format is reminiscent of
class called InnerOne declared in a package called OuterOne. This point of view is not entirely
inappropriate, an inner class belongs to its enclosing class in a fashion similar to the way
class belongs to a package. It is illegal for a class and to have the same name, so there
be no ambiguity.

![](bbox=[0.166, 0.723, 0.263, 0.758])

Although the dotted representation of inner class names for the declara-
ton of an identifier, it does not reflect the filename of the class. If you
try to load this class using Class.forName() method, the call will fail. On the
disk, and from the point of view of the Class class and class loaders, the name of
class is OuterOne.InnerOne. The dot-separated name is also used if you
print out the class name by using getClass().getName() on an
instance of an inner class. You probably recall that classes are loaded from Direc-
tories that reflect their package names. The dotted-separated convention
adopter inner class names to ensure there is no ambiguity in the dot
ween inner classes and package members. It also reduces conflicts with file
systems and shell interpreters that treat the dot character as special, perhaps
limiting the number of characters that can follow.