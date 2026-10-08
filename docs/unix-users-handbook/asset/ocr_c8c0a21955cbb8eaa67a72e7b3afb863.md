This causes the preprocessor to include the iostream.h file in the program. The old style specification uses a file name. This is not the case for the newer C++ standard.

The newer C++ standard does not specify file names for header files, they specify standard identifiers. The headers are an abstraction that ensures the appropriate information required by the program is included. The identifiers may or may not map to a file name. An example is as follows:

```
#include <iostream>
```

When including the newer style C++ headers, the contents of the headers are contained in the std namespace. For more information regarding namespaces, see the “Namespace” section later in this chapter.

# Enumerations

In C++, when declaring a variable of type enumeration Week, the following statement:

```
enum Week yesterday;
```

can be written as:

```
Week yesterday;
```

# Precedence

The precedence of a few new operators needs to be included. Scope resolution (::) has the highest order of precedence; see the “Namespace” section later in this chapter for more information. C++ has included four new casting operators; see the “Casting Operators” section later in this chapter for more information.

Table 14-7 lists operators in their order of precedence, starting with the highest precedence.