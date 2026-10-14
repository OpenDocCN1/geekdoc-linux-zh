# LOADING THE BASES

Deriving a class from multiple base classes is easy. As many C++ books show, simply inherit two or more base classes using a declaration such as

```
class D: public A, public B, private C {
// ... class contents
};
```

In this example, the new, derived class D inherits three classes, A, B, and C. It specifies that members in A and B retain their private, protected, and public access status in the new class, but that all members of C are to become private members of D.

The trouble with the foregoing example is that, although technically correct, it doesn't take reality into consideration. Chances are, unless you are the lucky type, some names in A, B, and C will conflict. For instance, suppose that classes A and B each have a public Display() member function. To decide which function to call requires using the class name and C++ scope resolution operator in statements such as these:

```
Display();  // ??? Ambiguous. Won't compile.
A::Display();  // Call A's Display() function
B::Display();  // Call B's Display() function
```

Unless class D declares its own Display() function, the first line doesn't compile. As shown, to resolve the name conflict among multiple Display() functions, you must use designations such as A:: and B::. This works, but is messy, and it places the responsibility of calling the correct function on the programmer—a requirement that object-oriented programming is supposed to help you avoid.

# USING MULTIPLE BASE CLASS CONSTRUCTORS

When inheriting from multiple base classes, you must be careful to create constructors that initialize all inherited elements. In general, you might declare the derived class and its constructor like this:

```
class D: public A, public B, private C {
public:
  D(): A(), B(), C() { }
};
```

The constructor D() calls the constructors for the three inherited classes, but in this case, it performs no other actions so its statement block is empty. Again, the code seems simple enough at first. However, C++ specifies that the constructors are called in the order listed. If one class object depends on one of the others, the resulting conflict can cause impossibly confusing results. This can happen particularly when classes declare themselves to be friends of other classes, a topic for Chapter 18, "Overloading Your Friends" in Part IV, "Advanced C++ Techniques." To avoid this type of trouble, try to create classes that operate as independently as possible—good advice whether or not you intend to use multiple inheritance.