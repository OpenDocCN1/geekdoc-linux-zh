
# Object Reference Conversion 113

This is the general format of an assignment conversion from an Oldtype to a Newtype. Unfortunately, Old-type can be a class, an interface, or an array; Newtype can also be a class, an interface, or an array. Thus there are nine (= 3... 3) possible combinations to consider. Figure 4.6 shows the rules for all nine cases.

It would be difficult to memorize the nine rules shown in Figure 4.6. Fortunately, there is a rule of thumb.

Recall that with primitives, conversions were permitted, provided they were widening—the notion of widening does not really apply to references, but a similar principle is at work. In general, object reference conversion is permitted when the direction of the conversion is “up” the inheritance hierarchy; that, the old type should inherit from the new type. This rule of thumb does not cover all nine cases, but it is a helpful to look at things.

The rules for object reference conversion can be stated as follows:

- An interface type can be converted only to an interface type or Object. If the new type is an interface, it must be a super of the old type.
- A class type can be converted to a class type or to an interface type. If converting to a class type, the new type must be a subclass of the old type. If converting to an interface type, the old class must implement the interface.
- An array may be converted to the class, to the interface Cloneable or Serializable, or to an array. Any array of object reference types can be converted to an array, and the old element type must be convertible to the new element type.

To illustrate these rules, consider the inheritance hierarchy shown in Figure 4.7 (assume there is an interface called Squeezeable).

# FIGURE 4.6 The rules for object reference assignment conversion

| Oldtype is a class | Oldtype is an interface | Oldtype is an array |
|---|---|---|---|
| Newtype is a class | Oldtype must be a subclass of Newtype | Newtype must be Object | Newtype must be Object |
| Newtype is an interface | Oldtype must implement interface Newtype | Oldtype must be a subinterface of Newtype | Newtype must be Cloneable or Serializable |
| Newtype is an array | Compiler error | Compiler error | Oldtype must be an array of some object reference type that can be converted to whatever Newtype is an array of |

Converting Oldtype to Newtype:

# FIGURE 4.7 A simple class hierarchy

![](img/09f8389b7ae2705d1ab14be2d5e857e3_148_0.png)

As a first example, consider the following code:

1. Tangelo tange = new Tangelo();
2. Citrus cit = tange;

This code is fine. A Tangelo is being converted to a Citrus. The new type is a superclass of the old type, so the conversion is allowed. Converting in the other direction (“down” the hierarchy tree) is not allowed:

1. Citrus cit = new Citrus();
2. Tangelo tange = cit;

This code will result in a compiler error.
What happens when one of the types is an interface?

1. Grapefruit g = new Grapefruit();
2. Squeezable squee = g; // No problem
3. Grapefruit g2 = squee; // Error

The second line (“No”) changes a class type (Grapefruit) to an interface type. This is correct, provided Grapefruit really implements Squeezable. A glance at Figure 4.7 shows that this is indeed the case, because Grapefruit inherits from Citrus, which implements Squeezable. The third line is an error, because an interface can never be implicitly converted to any reference type other than Object.

Finally, consider an example with arrays;

1. Fruit fruits[];
2. Lemon lemons[];
3. Citrus citruses[] = new Citrus[10];
4. for (int i = 0; i < 10; i++) {
5. citruses[i] = new Citrus();
6. }
7. fruits = citruses; // No problem
8. lemons = citruses; // Error

Line 7 converts an array of Fruit. This is fine, because Fruit is a superclass of Citrus. Line 8 converts in the other direction and fails, because Lemon is not a superclass of Citrus.

# Object Method-Class Conversion

Fortunately, the rules for method-call conversion of object reference values are the same as the rules described for assignment of objects. The general rule of thumb is that converting to a superclass is permitted and converting to a subclass is not permitted.
To see how the rules make sense in the context of method calls, consider the extremely useful java.lang.Vector class. You can store anything in a vector (anything nonprimitive, that is) by calling the adding method (Object obj). For example, the following code stores a Tangelo in a vector:

1. Vector myVec = new Vector();
2. Tangelo mange = new Tangelo();
3. myVec.add(tange);

The argument will automatically be converted to type Object. The automatic conversion means that the people who wrote the java.lang.Vector class didn't have to write a separate method for every possible type of object that anyone might want to store in a vector. This is fortunate: the Tangelo class was developed years after the invention of the vector, so the developer of the Vector class could not possibly have written specific Tangelo-handling code. An object of any class (and even an array of type) can be passed into the single add (Object obj) method.

# Object Reference Casting

Object reference casting is like primitive casting: by using a cast, you convince the compiler to let you do a conversion that otherwise might not be.

Any kind of conversion is allowed for assignments or method calls is allowed for explicit casting. For example, the following code is legal:

1. Lemon lem = new Lemon();
2. Citrus cit = (Citrus)lem;

The cast is legal but not needed; if you leave it out, the compiler will do an implicit assignment conversion. The power of casting appears when you explicitly cast to a type that is not allowed by the rules of implicit conversion.
Understand the difference between objects and object reference variables. Every object (well, nearly every object—there are obscure cases) is constructed via the new operator. The class name following new determines for all time the true class of the object. If an object is constructed by calling new Color(222, 0, 255), then throughout that object's life, its class will be Color.
Java programs do not deal directly with objects. They deal with references to objects. For example, consider the following code:

Color purple = new Color(222, 0, 255);

The variable purple is not an object; it is a reference to an object. The object itself lives in memory somewhere in the Java Virtual Machine (JVM). The variable purple contains something similar to the address of the object. This address is known as a reference to the object. The difference between a reference and an object is illustrated in Figure 4.8. References are stored in variables, and variables have types that are specified by the programmer at compile time. Object reference types can be classes (such as Graphics or FileWriter), interfaces (such as Runnable or LayoutManager), or arrays (such as int[] or Vector[]).

# FIGURE 4.8 Reference and object

![](img/09f8389b7ae2705d1ab14be2d5e857e3_150_0.png)

# Object Reference Casting

Although an object's class is unchanging, it may be referenced by variables of different types. For example, consider a stack. It is constructed by calling new Stack(), so its class really is Stack. Yet at various moments during the lifetime of this object, it may be referenced by variables of type Stack (of course), or of Vector (Stack inherits from Vector), or of Object (because everything inherits from Object). It may even be referenced by variables of type Serializable, which is an interface, because the Stack class implements the Serializable interface. This situation is shown in Figure 4.9.

# FIGURE 4.9 Many variable types, one class

![](img/09f8389b7ae2705d1ab14be2d5e857e3_151_0.png)

Few rules govern object casting because a large number of obscure cases must be covered. For the exam, the important rules to remember when casting from Old1type to Newtype are as follows:

- When both Old1type and Newtype are classes, one class must be a subclass of the other.
- When both Old1type and Newtype are arrays, both arrays must contain reference types (not primitives), and it must be legal to cast an element of Old1type to an element of Newtype.
- You can always cast between an interface and a nonfinal object.
