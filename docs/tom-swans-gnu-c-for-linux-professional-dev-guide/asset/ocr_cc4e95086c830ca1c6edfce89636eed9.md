```
```cpp
Two obj2;
obj2.Show(obj1);
}

void Two::Show(One obj1)
{
    cout << obj1.s1 << s2 << endl;
}
```
```

The program’s output is the same as friendfn.cpp, but it uses a different technique to provide access to private data. Compile and run the program with the commands:

$ g++ friendfn.cpp
$ ./a.out
Testing one, two, three

The new program, friendfm.cpp, is similar to friendfn.cpp but uses a friend member function to access the private members of two classes. As in the other program, the new code declares two classes—One and Two. In this case, however, class Two declares Show() as a common public member function. Class One declares that same member function as a friend, using the class name Two and C++ scope resolution operator to tell the compiler where to find this function:

friend void Two::Show(One &c1);

Given that declaration, function Two::Show() is a friend of class One and can therefore access One’s private and protected members. The order of the two classes is reversed from the earlier listing because the class that prototypes the member function must be declared before the class that specifies the member function as a friend. For One to declare Two::Show() as a friend of the class, the compiler must already have seen Two’s declaration.

Another difference is the way Show() refers to private data in the two classes. (Refer to the function implementation at the end of Listing 18.4.) The function now declares only one reference parameter, obj1, of the One class. Because Show() is a member of class Two, it can access all members of Two directly. However, the expression obj1.s1 in the output statement is allowed because Show() is a friend of class One, of which s1 is a private data member.

# SUMMARY

A class may declare another class or function as a friend. This gives the friend access to the declaring class’s normally private and protected members. Because friends break the very rules that help authors write robust C++ programs, experienced programmers use them only when absolutely necessary. However, friends are useful in some cases—for example, in creating overloaded operators, the subject of the next chapter.

For more information on subjects introduced in this chapter, turn to the following chapters:

+   - Chapter 13, “Creating and Destroying Objects”
+   - Chapter 19, “Overloading Operators”