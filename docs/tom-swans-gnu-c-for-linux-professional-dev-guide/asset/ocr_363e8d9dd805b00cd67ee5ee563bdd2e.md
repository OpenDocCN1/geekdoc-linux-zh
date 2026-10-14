Be sure not to follow the function name with parentheses. You merely want to refer to the function by name, not to call it. Either way, to use the pointer, follow these two rules:

+   1. Refer to an object of the class (unless the function is static).
+   2. Surround the function call with parentheses.

If data is an int variable, and object is a TAnyClass object, the following statement copies to data the result returned by GetValue() using a member function pointer:

```
int data = (object.*myfnptr)();
```

The period and asterisk is one C++ symbol, called the pointer-to-member operator. It is used to dereference a member function pointer for a class object. The parentheses in the expression (object.*myfnptr) are necessary because the function-call operator—a set of empty parentheses—has higher precedence than the pointer-to-member operator. The preceding statement is equivalent to the following:

```
int data = object.GetValue();
```

You can also call member functions by using a pointer for objects themselves addressed by pointers. For example, in the sample program, a statement assigns to pointer fp the address of a TAnyClass object created by the new operator:

```
TAnyClass *fp = new TAnyClass(object);
```

Following this, the next expression calls GetValue() by using the member function pointer:

```
(fp->*myfnptr)();
```

The triple-character symbol ->* is a variation of the pointer-to-member operator. Again, extra parentheses are needed because () has higher precedence than ->*. The preceding statement is equivalent to this:

```
fp->GetValue();
```

# STATIC MEMBER FUNCTIONS

Chapter 14, "Investing in Inheritance," introduces static members. In brief, a static data member exists for all objects of a class, as compared to a nonstatic member that is allocated space in every class object. Member functions may also be static. Unlike a nonstatic member function, a static function is not called in reference to an object but solely in reference to the class. This can be useful for designing functions that initialize a value or perform some other action that affects all subsequently constructed objects. To declare a static member function, precede its prototype with the reserved word static:

```
class TAnyClass {
public:
    static void GlobalInit();
    ...
};
```