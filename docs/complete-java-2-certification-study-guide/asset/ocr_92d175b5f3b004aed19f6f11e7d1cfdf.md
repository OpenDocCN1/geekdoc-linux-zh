# The Arithmetic Operators 47

Where either the operands of a + expression a String object, the meaning of the operator is changed from numeric addition to string concatenation. In order to achieve this result, operands must be handled as text. If both operands are in fact String objects, this is simple. If, one of the operands is not a String object, the non-String operand is converted to a String object before the concatenation takes place.

For object types, conversion to a String is performed by invoking the toString() method of that object. The toString() method is defined in java.lang.Object, which is the root of the class hierarchy, and therefore all objects inherit a toString() method. Sometimes, the effect of the toString() method is to produce cryptic text that is suitable only for debugging output, but ultimately exists and may be called.

Conversion of an primitive type to a String is typically achieved by using, indeed, the conversion methods in the wrapper classes. For example, an int value is converted by the static method Integer.toString().

The toString() method in java.lang.Class returns a String that contains the name of the object and some identifying value—typically its reference value, separated by the symbol (@). For example, this String might look like java.lang.Object@1lc6dd3. This behavior is inherited by subclasses unless they deliberately override it.

> It is a good idea to define a helpful toString() method in all your classes, even if you do not require it as part of the class behavior. The toString() method that it represents the state of the object in a fashion that can assist in debugging; for example, output the names and values of the main instance variables.

![](bbox=[0.139, 0.463, 0.203, 0.503])

To prepare for the Certification Exam questions, and to use the + operator effectively in your programs, you should understand the following points:

+   - For a + expression with two operands of primitive numeric type, the result
- Is of a primitive numeric type.
- Is at least int, because of normal promotions.
- Is of a type at least wide as the wider of the two operands.
- Has a value calculated by promoting the operands to the result and then performing the addition using that type. This might result in overflow or loss of precision.
- For a + expression with any operand that is not of primitive numeric type,
- At least one operand is a String object or literal; otherwise, the expression is illegal.
- Any remaining non-String operands are converted to String, and the result of the expression is the concatenation of all operands.
- To convert an operand of some object type to a String, the conversion is performed by invoking the toString() method of that object.
- To convert an operand of a primitive type to a String, the conversion is performed by a static method in a container class, such as Integer.toString().