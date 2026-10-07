# Object Reference Casting 119

This code has four references but only one object. The object c is Grapefruit, because Grapefruit's constructor is called on line 4. The assignment c = g on line 5 is a perfectly legal assignment conversion (“up the inheritance hierarchy), so no explicit cast is required. In lines 6 and 7, the Citrus is cast to Grapefruit and to a Tangerelo. Recall that for casting between classes, one of the two (it doesn't matter which) must be a subclass of the other. The first cast is from Citrus to its subclass Grapefruit; the second is from Citrus to its subclass Tangerelo at compile time. Thus both casts are legal—but the compiler cannot determine the object referenced by c, so it accepts both casts and lets fate determine the outcome at runtime.

When the code is executed, eventually the JVM determines to execute line 6: g1 = (Grapefruit)c;. The class of c is determined to be Grapefruit, and there is no object converting a Grapefruit to a grapefruit.

Line 7 attempts (at runtime) to cast c to type Tangerelo. The class of c is still Grapefruit, and a Grapefruit cannot be cast to a Tangerelo. In order for the cast to be legal, the class of c would have to be Tangerelo itself or subclass of it. Because this is not the case, a runtime exception (java.lang.ClassCastException) is thrown.

Now take an example where an object is an interface type. Begin by considering the following code:

+   1. Grapefruit, g1;
2. Squeezeable s;
3. g = new Grapefruit();
4. s = g; // Convert Grapefruit to Squeezeable (OK)
5. g1 = s; // Convert Squeezeable to Grapefruit
// (Compile error)

This code will not compile. Line 5 attempts to convert an interface (Squeezeable) to a class (Grapefruit). It doesn't matter that Grapefruit implements Squeezeable. Implicitly converting an interface to a class is never allowed; it is one of those cases where you have to use an explicit cast to tell the compiler that you know what you're doing. With the cast, line 5 becomes

+   5. g = (Grapefruit)s;

Adding the cast makes the compiler happy. At runtime, the JVM checks whether the class of s (which is Grapefruit) can be converted to Grapefruit. It certainly can, so the case is allowed. For a final example, involving arrays, look at the following code:

+   1. Grapefruit g[];
2. Squeezeable s[];
3. Citrus c[];
4. g = new Grapefruit[500];
5. s = g; // Convert Grapefruit array to
// Squeezeable array (OK)
6. c = (Citrus[])s; // Cast Squeezeable array to Citrus
// array (OK)