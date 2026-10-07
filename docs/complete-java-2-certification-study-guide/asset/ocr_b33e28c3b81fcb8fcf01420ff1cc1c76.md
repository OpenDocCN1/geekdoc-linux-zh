Finally, consider an example with arrays;

+   1. Fruit fruits[];
2. Lemon lemons[];
3. Citrus citruses[] = new Citrus[10];
4. for (int i = 0; i < i++) {
5. citruses[i] = new Citrus();
6. )
7. fruits = citruses; // No problem
8. lemons = citruses; // Error

Line 7 converts an array of Fruit. This is fine, because Fruit is a super-class of Citrus. Line 8 converts in the other direction and fails, because Lemon is not a superclass of Citrus.

# Object Method-Class Conversion

Fortunately, the rules for method-call conversion of object reference values are the same as the rules described for assignment of objects. The general rule of thumb is that converting to a superclass is permitted and converting to a subclass is not permitted.
To see how the rules make sense in the context of method calls, consider the extremely useful java.lang.Vector class. You can store anything in a vector (anything nonprimitive, that is) by calling the adding method (Object obj). For example, the following code stores a Tangelo in a vector:

+   1. Vector myVec = new Vector();
2. Tangelo mange = new Tangelo();
3. myVec.add(tange);

The argument will automatically be converted to type Object. The automatic conversion means that the people who wrote the java.lang.Vector class didn't have to write a separate method for every possible type of object that anyone might want to store in a vector. This is fortunate: the Tangelo class was developed years after the invention of the vector, so the developer of the Vector class could not possibly have written specific Tangelo-handling code. An object of any class (and even an array of type) can be passed into the single add (Object obj) method.

# Object Reference Casting

Object reference casting is like primitive casting: by using a cast, you convince the compiler to let you do a conversion that otherwise might not be.