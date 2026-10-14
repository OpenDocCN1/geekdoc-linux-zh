Operator overloading makes it possible to add and subtract objects that store integer values in string form. To make this happen, we find two functions in the TStrOp class overload the plus and minus operators. The two functions are declared as the public members:

```
friend long operator+(TStrOp a, TStrOp b);\nfriend long operator-(TStrOp a, TStrOp b);
```

So that TStrOp objects can participate in expressions involving other integer values, each operator returns type long. Each is a binary operator, so it receives two argument values, both objects of the TStrOp class. Examine the overloaded operator implementations following main(). Because the functions are friends, they do not require qualification with their class names but are implemented as other common C++ functions. Also, because they are friends, they can directly access the private data member string in the TStrOp class. For example, to convert object a’s value to a long integer, the function uses the following expression:

```
atol(a.value.c_str());
```

That passes the C-style string of the string-class object value in object a to the standard atol() function, resulting in the string’s equivalent integer value. Because the overloaded operator functions are friends of the class, they can access the private data members a.value and b.value.

![](bbox=[0.113, 0.456, 0.939, 0.519])

# OVERLOADED CLASS MEMBER OPERATORS

Overloaded functions also can be members of a class, as Listing 19.2, strops2.cpp, demonstrates. The program is similar to the strops.cpp demonstration in the preceding section, but illustrates how to overload operators using class member functions instead of friends.

```
LISTING 19.2    STROPS2.CPP\n\n#include <iostream.h>\n#include <stdlib.h>    // Need atol()\n#include <string.h>    // Need string class\n\nclass TStrOp {\nprivate:\n    string value;\npublic:\n    TStrOp(): value("0") { }\n    TStrOp(string(arg) : value(arg) { }\n    long GetValue() { return atol( value.c_str() ); }\n    long operator+(TStrOp b);\n    long operator-(TStrOp b);\n};\n\nint main()\n{
```