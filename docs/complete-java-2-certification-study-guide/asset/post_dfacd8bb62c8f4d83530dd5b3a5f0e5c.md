
# Chapter 6 • Objects and Classes

11. Which of the following override method whose signature is void xyz(float f)?

-   A. void xyz(float f)
-   B. public void xyz(float f)
-   C. private void xyz(float f)
-   D. public int xyz(float f)
-   E. private int xyz(float f)

12. Which of the following are true? (Choose all that apply.)

-   A. An enum definition should declare that it extends java.lang.Enum.
-   B. An enum may be subclassed.
-   C. An enum may contain public method definitions.
-   D. An enum may contain private data.

13. Which of the following are true? (Choose all that apply.)

-   A. An enum definition may contain the main() method of an application.
-   B. You can call an enum's toString() method.
-   C. You can call an enum's wait() method.
-   D. You can call an enum's notify() method.

14. Suppose x and y are of type TrafficLight, which is an enum. What is the best way to test x and y refer to the same constant?

-   A. if (x == y)
-   B. if (x.equals(y))
-   C. if (x.toString().equals(y.toString()))
-   D. if (x.hashCode() == y.hashCode())

15. Which of the following restrictions apply to anonymous inner classes?

-   A. They must be defined inside a code block.
-   B. They may only read and write final variables of the enclosing class.
-   C. They may only call final methods of the enclosing class.
-   D. They may not call the enclosing class synchronized methods.

16. Given the following code, which of the following will compile?
```java
enum Spice { NUTMEG, CINNAMON, CORIANDER, ROSEMARY; }
```

-   A. Spice sp = Spice.NUTMEG; Object ob = sp;
-   B. Spice sp = Spice.NUTMEG; Object ob = (Object)sp;
-   C. Object ob = new Object(); Spice sp = object;
-   D. Object ob = new Object(); Spice sp = (Spice)object;

## 17. Which of the following are true?

-   A. An anonymous inner class may implement at most one interface.
-   B. An anonymous inner class may implement arbitrarily many interfaces.
-   C. An anonymous inner class may extend a parent class other than Object.
-   D. An anonymous inner class that implements one interface may extend a parent class other than Object.
-   E. An anonymous inner class that implements several interfaces may extend a parent class other than Object.

## 18. Which methods return an enum constant's name?

-   A. getName()
-   B. name()
-   C. toString()
-   D. toString()
-   E. getString()

# 19. Suppose class X contains the following method:

```java
void doSomething(int a, float b) { ... }
```

Which of the following methods may appear in class Y, which extends X?

-   A. public void doSomething(int a, float b) { }
-   B. private void doSomething(int a, float b) { }
-   C. public void doSomething(int a, float b) throws java.io.IOException { }
-   D. private void doSomething(int a, float b) throws java.io.IOException { }

# 20. This question involves IOException, AWTException, and EOFException. They are all checked exception types. IOException and AWTException extend Exception, and EOFException extends IOException. Suppose class X contains the following method:

```java
void doSomething() throws IOException { ... }
```

Which of the following methods may appear in class Y, which extends X?

-   A. void doSomething() { }
-   B. void doSomething() throws AWTException { }
-   C. void doSomething() throws EOFException { }
-   D. void doSomething() throws IOException, EOFException { }

# Answers to Review Questions

-   1. A, C, E. In each of these, the argument list differs from the original, the method is an overload. Overloaded methods are effectively independent, and there are no constraints on the accessibility, return type, or exceptions that may be. B would be a legal overriding method, except that it cannot be [private].
-   2. C, D. An enum cannot extend another class or be subclassed, but it can contain public methods and private data.
-   3. A, B, C, D. Enums can have a main method, and they inherit from Object, so they have toString(), wait(), and notify().
-   4. A. Since enum constants are constants, the == operator is the most reliable and fastest way to compare them.
-   5. A. Anonymous inner classes must be defined in a block. There are no other restrictions on accessing non-final members of the enclosing class.
-   6. A, B. Spice is a subclass of Object, so it can be assigned to Object. C and D are illegal due to type mismatches.
-   7. B, C, D. An inner class can implement multiple interfaces or extend one parent class, but not both at the once.
-   8. B. The name() method is specifically designed to return the name of the enum constant.
-   9. A, B, C. Overriding allows changing access levels (making them broader) or adding exceptions, but not narrowing them or removing them.
-   10. A, B, C, D. A subclass method can remove an exception or add more specific exceptions, but not throw broader ones.
