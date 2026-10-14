(They may also be of related classes, as Chapter 14, "Investing in Inheritance" explains.) The following statement creates a TDate object named t4 using a copy of t3's value:

TDate t4( t3 );

That creates a new object, t4, and copies to it the value of t3. The statement is equivalent to the following native type declaration, which creates a double variable t4 and assigns to it the value of f3:

double f4(f3);

The fifth and final method for constructing a class object also copies one object to another:

TDate t5 = t4;

That creates a new TDate object, t5, equal to the value of t4. This is exactly the same as the preceding method but uses the more intuitive assignment operator. It is exactly equivalent to the native type statement:

double f5 = f4;

# THE DEFAULT CONSTRUCTOR

A default constructor has no parameters and, like all constructors, is named the same as its class. In the sample construct.cpp program, the TDate() default constructor is implemented separately as follows (I moved the individual statements to one line to save space here):

```
TDate::TDate()
{
    dt_month = 0;  dt_day = 0;   dt_year = 0;
}
```

Elsewhere in the program, creating an object with no arguments calls the default constructor, which assigns zero to each data member in the object. The default TDate() constructor makes possible declarations such as

TDate t1;

That calls the TDate() default constructor to initialize the t1 object. Unlike native type variables, however, this happens whether or not the preceding declaration is inside a function—a subtle but important difference between declarations of class objects and those of native types. Class objects are always initialized by a constructor. A native type variable that is local to a function is uninitialized until assigned a value.

# THE COPY CONSTRUCTOR

Statements that cause one object to be copied to a newly created object call a special constructor known as the copy constructor. This happens when you create objects using statements such as the following (remember, however, the third statement, although allowed, is impractical because it wastefully creates a temporary object):

```
TDate t4(t3);
TDate t5 = t4;
TDate t2 = TDate(12, 31, 1999);  // ???
```