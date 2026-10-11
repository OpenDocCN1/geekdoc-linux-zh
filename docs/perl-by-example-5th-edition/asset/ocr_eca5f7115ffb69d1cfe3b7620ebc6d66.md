EXPLANATION
1 The package Grandpa is declared.
2 The subroutine greetme is defined in this package.
3 The package Parent is declared. It is empty.
4 The package Child is declared.
5 This line is printed to show the flow of execution in the program.
6 The greetme subroutine is called as one of the Parent package methods. Since the method could not be found in its own class or in the @ISA array, and an AUTOLOAD function is not supplied in the Parent package, Perl looks for package UNIVERSAL as a last resort.
7 This is the built-in base called UNIVERSAL. All modules inherit from UNIVERSAL which is implicitly on the end of the @ISA array.
8 The AUTOLOAD function will automatically be called from the UNIVERSAL class.
9, 10 Within the AUTOLOAD function, the greetme function in the Grandpa package will be invoked.

# 14.4.3 Derived Classes

As already discussed, inheritance is when one class can inherit methods from an existing class. The existing class is called the base, parent, or superclass, and the new class that inherits from it is called the derived, child, or subclass. The base class has capabilities that all its derived classes inherit, and the derived classes can go beyond these capabilities.

If a derived class inherits from one base class, it is called single inheritance. For example, single inheritance in real life might be that a child inherits his ability to draw from his father. If a derived or subclass inherits from more than one base class, this is called multiple inheritance. To continue the analogy, the child inherits his ability to draw from his father and his ability to sing from his mother. In Perl, the derived class inherits methods from its base class and can add and modify these methods when necessary.

The classes are inherited by putting them in the @ISA array. In Chapter 13, "Modularize It, Package It, and Send It to the Library!" we looked at modules from the Perl standard library and modules you could create yourself. In order to include a module or pragma into your program, the use function was called with the module name (minus the .pm extension). The module had the capability of exporting symbols to other packages that might need to use the module. A special module called Exporter.pm handled the details for exporting and importing symbols between modules and the symbols were listed in the @EXPORT and @EXPORT_OK arrays. The Exporter.pm module, you may recall, was listed in the @ISA array in order to inherit methods necessary for it to do its job. But if a module functions as a class, then its methods can be called without using Exporter. Note in the following examples, the class methods and the instance methods are not exported.

The following examples demonstrate inheritance. The user program need not make any reference to the base class, Employee. The Salesman class and the Teacher class are derived from Employee. The Salesman and Teacher class "use" the Employee class. Figure 14.5 shows this inheritance hierarchy graphically.