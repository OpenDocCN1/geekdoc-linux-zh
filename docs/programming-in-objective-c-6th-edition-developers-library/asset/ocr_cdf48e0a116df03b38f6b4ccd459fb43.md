The method is preceded by the notation F to identify that it belongs to the F class.

A new instance of a F is created like a normal variable in C, as in the following declaration in m:

```
```
F
```
```

The numerator and denominator of the fraction are then set to 1 and 3, respectively, with the following method calls:

```
```
m
```
```

The value of the fraction is then displayed using the fraction's p method.

Probably the oddest-appearing statement from Program 18.3 occurs inside the p method as follows:

> > Click here to view code image

```
```
s
```
```

c is the name of the standard output stream, analogous to σ in C. The < is known as the stream insertion operator, and it provides an easy way to get output. You might recall that < is also C's left shift operator. This is one significant aspect of C++: a feature known as operator overloading that allows you to define operators that are associated with a class. Here, the left shift operator is overloaded so that when it is used in this context (that is, with a stream as its left operand), it invokes a method to write a formatted value to an output stream, instead of trying to actually perform a left shift operation.

As another example of overloading, you might want to override the addition operator + so that if you try to add two fractions together, as in

```
```
m
```
```

an appropriate method from your F class is invoked to handle the addition.

Each expression that follows the < is evaluated and written to the standard output stream. In this case, first the string " gets written, followed by the fraction's numerator, followed by a /, the fraction's denominator, and then a newline character.

The C++ language is rich with features. Consult Appendix E, “Resources,” for recommendations on a good tutorial.

Note that in the previous C++ example, the getter methods N and D were defined in the F class but were not used.

# ## Defining a C# Class to Work with Fractions

As the final example in this chapter, Program 18.4 shows the fraction example written in C#, a programming language developed by Microsoft, Inc. C# is part of Microsoft's Visual Studio suite and is a key development tool in the .NET Framework. If you want to try C#, visit www.visualstudio.com/en-US/products/visual-studio-o-express-vs to download a free express version of the full product.