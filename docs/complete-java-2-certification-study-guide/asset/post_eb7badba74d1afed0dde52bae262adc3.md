
Inner classes can give your programs additional clarity and make them concise. Inner class in class scope can have any accessibility, including private. Inner classes defined local to a block may not be static. However, an inner class declared to a block (for example, in a method) must not have any access modifier. A class is effectively private to the block. Classes defined in methods can be anonymous, in which case they must be instantiated at the same point they are defined. Anonymous inner classes can implement an interface or extend a class, but they cannot have explicit constructors.

Contracts are agreements among programmers regarding class behavior. Classes that honor contracts will interact predictably with other classes.

Finally, we looked at enums, which are specialized classes that provide a robust alternative to enumerated constants. Enums are never explicitly constructed.

## Exam Essentials

- Be familiar with the way the Java language realizes the “is a” and “has a” relationships. The “is a” relationship implies class extension. The “has a” relationship implies ownership of a reference to a different object.

- Be able to identify legally overloaded methods and constructors. The methods/constructors must have different argument lists.

- Be able to identify legally overridden methods. The methods must have the same name, argument list, and return type.

- Know the return types for overloaded and overridden methods. There are no restrictions for an overloaded method; an overriding method must have the same return type as the overridden version.

- Know that the compiler generates a default constructor when a class has no explicit constructors. When a class has constructor code, no default constructor is generated.

- Understand the chain of calls to parental constructors. Each constructor invocation begins by invoking a parental constructor.

- Know how to create a constructor that invokes a nondefault parental constructor. Understand the use of the `super` keyword.

- Be able to identify correctly constructed inner classes, including inner classes in methods and anonymous inner classes. The syntax for each of these forms is explained in previous sections of this chapter.

- Know which data and methods of an enclosing class are available to an inner class. Understand that the inner class can access all data and methods of its enclosing class.

- Understand the restrictions on static inner classes. Understand that a static inner class cannot access nonstatic features of its enclosing class.

- Know how to use a nonstatic inner class from a static method of the enclosing class. Be able to recognize the new `Outer().new Inner()` format.

- Know how to use enums, and when it is appropriate to use them. Enums are classes that are intended to replace enumerated constants. You should be able to recognize an (old-style) group of enumerated constants and know how to create appropriate enums to replace the constants.

## Review Questions

- 1. Consider this class:

```java
1. public class float Test1 {
2.   public float aMethod(float a, float b) {
3. }
4 
5. }
```

Which of the following methods would be legal if added (individually) at line 4? (Choose that apply.)

- A. public int aMethod(int a, int b) { }
- B. public float aMethod(float a, float b) { }
- C. public float aMethod(float a, float b, int c) throws Exception { }
- D. public float aMethod(float c, float d) { }
- E. private float aMethod(int a, int b, int c) { }

> Consider these classes, defined in separate source files:

- 1. public class Test1 {
```java
2.   public float aMethod(float a, float b)
3.     throws IOException ...
5. }
```

- 1. public class Test2 extends Test1 {
```java
2.
3. }
```

> Which of the following methods would be legal (individually) at line 2 in class Test2? (Choose that apply.)

- A. float aMethod(float a, float b) {...}
- B. public int aMethod(int a, int b) throws Exception {...}
- C. public float aMethod(float a, float b) throws Exception {...}
- D. public float aMethod(float p, float q) {...}

- 3. You have been given a design document for a veterinary registration system for implementation in Java. It states:

> “A pet has an owner, a registration date, and a vaccination-due date. A cat is a pet that has a flag indicating whether it has been neutered, and a textual description of its markings.”

Given that the Pet has already been defined, which of the following fields will be appropriate for inclusion in Cat as members? (Choose all apply.)

- A. pet;
- B. Date registered;
- C. Date vaccinationDue;
- D. Cat;
- E. boolean neutered;
- F. String markings;

- 4. You have been given a design document for veterinary registration system for implementation in Java. It states:

> “A pet has an owner, a registration date, and a vaccination-due date. A cat is a pet that has a flag indicating whether it has been neutered, and a textual description of its markings.”

Given that the Pet has already defined and you expect the Cat class to be used freely throughout the application, how would you make the declaration of the Cat up to not including the first brace? Use only these words: boolean, class, Date, extends, Object, Pet, private, protected, public, String.

- A. protected class extends Owner
- B. public class extends Object
- C. public class extends Pet
- D. private class extends Pet

- 5. Consider the following classes, declared in separate files:
```java
1. public class Base {
2.   public void method(int i) {
3.   System.out.print("Value is " + i);
4.   }
5. }

1. public class Sub extends Base {
2.   public void method(int j) {
3.   System.out.print("This value is " + j);
4. }
5.   public void method(String s) {
6.   System.out.print("I passed " + s);
7. }
8.   public static void main(String args[]) {
9.   Base b1 = new Base();
10.  Base b2 = new Sub();
11.  b1.method(5);
12.  b2.method(6);
13. }
14. }
```

What output results when the main method of class Sub is run?

- A. Value is 5Value is 6
- B. This value is 5value is 6
- C. Value is 5value is 6
- D. This value is 5Value is 6
- E. I passed 5I 6

- 6. Consider the following class definition:
```java
1. public class Test extends Base
2.   public Test(int j)
3. }
4.   public Test(int j, int k) {
5.   super(j, k);
6. }
7. }
```

Which of the following are legitimate calls to construct instances of the Test class? (Choose all apply.)

- A. Test t = new Test()
- B. Test t = new Test(1);
- C. Test t = new Test(1, 2);
- D. Test t = new Test(1, 2, 3);
- E. Test t = (new Base()).new Test(1);

- 7. Consider the following class definition:
```java
1. public class Test extends Base {
2.   public Test(int j) {
3.   }
4.   public Test(int j, int k) {
5.   super(j, k);
6.   }
7. }
```

Which of the following forms of constructor must exist explicitly in the definition of the Base class? Assume Test and Base are in the same package. (Choose all apply.)

- A. Base() { }
- B. Base(int j) { }
- C. Base(int j, int k) { }
- D. Base(int j, int k, l) { }

- 8. Consider the following class definition:
```java
1. public class Outer {
2.   private int a = 1;
3.   private int b = 2;
4.   private void method(final int c) {
5.   int d = 3;
6.   class Inner {
7.     private void iMethod(int e) {
8.     }
9.   }
10. }
11. }
```

Which variables can be referenced at line 8? (Choose all apply).

- A. a
- B. b
- C. c
- D. d
- E. e

- 9. Which of the following statements are true? (Choose all apply.)

- A. Given that Inner is a nonstatic class inside a public Outer and appropriate private constructors are defined, an instance of Inner can be constructed like this: new Outer().newInner()
- B. If an anonymous inner class inside the class Outer is defined to implement the interface ActionListener, it can be constructed like this: new Outer().newActionListener()
- C. Given that Inner is a nonstatic class declared inside a public Outer and appropriate private constructors are defined, an instance of Inner can be constructed in a static method like this: new Inner()
- D. An anonymous class instance that implements the interface MyInterface can be constructed and returned from a method like this:
1. return new MyInterface(int x) {
2. int x;
3. public MyInterface(int x) {
4. this.x = x; 6. }; };

- 10. Which of the following are legal errors?

- A. enum Animals { LION, TIGER, BEAR }
- B. enum Animals {
int age;
LION, TIGER, BEAR;
}
- C. enum Animals {
LION, TIGER, BEAR;
int weight;
}
- D. enum Animals {
LION(450), TIGER(450), BEAR;
int weight;
}

Animals(int w) {
weight = w;
}
