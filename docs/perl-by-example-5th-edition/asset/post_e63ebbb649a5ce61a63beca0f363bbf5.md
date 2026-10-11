
(class). If the method still isn't found, then Perl searches for an *AUTOLOAD* function and calls that method instead. And if that isn't found, then Perl searches for the last time in a special predefined package called *UNIVERSAL*. The *UNIVERSAL* class is a global base class for all packages, the highest class in the hierarchy of classes.

The `@ISA` array is not searched in a call to a normal subroutine but in a call to a subroutine if it is called with the method invocation syntax.

## EXAMPLE 14.16

```perl
#!/bin/perl
# Example of attempting inheritance without updating
# the @ISA array
1 { package Grandpa;
2   $name = "Gramps"; # Global package variable for Grandpa
3   sub greetme {
4     print "Hi $Child::name I'm your $name from package Grandpa.\n";
   }
   }
4 { package Parent;
   # This package is empty
   }
5 { package Child;
6   $name = "Baby";
7   print "Hi I'm $name in the Child Package here.\n";
8   Parent->greetme(); # Use method invocation syntax
   }
```

(Output)
Hi I'm Baby in the Child Package here.
Can't locate object method "greetme" via package "Parent" at
inher2 line 23.

## EXPLANATION

- 1. The package *Grandpa* is declared.
- 2. The global scalar `$name` is assigned *Gramps* in package *Grandpa*.
- 3. The subroutine *greetme* is defined and when called, the *print* statement will be executed. `$Child::name` refers to the global scalar `$name` in the *Child* package.
- 4. The package *Parent* is declared. It is empty.
- 5. The package *Child* is declared. This package will try to call a method from another package. Although objects and methods aren't being used here, the purpose of this example is to show you what happens if you try to insert a method from a class that this package doesn't know about.
- 8. Perl can't find the method *greetme* in package *Parent* and prints the error message.

## EXAMPLE 14.17

```perl
#!/bin/perl
# Example of attempting inheritance by updating the @ISA array
1 package Grandpa;
  $name = "Gramps";
2 sub greetme {
    print "Hi $Child::name I'm your $name from package Grandpa.\n";
}
3 { package Parent;
4   @ISA=qw(Grandpa); # Grandpa is a package in the @ISA array.
  # This package is empty.
}
5 { package Child;
  $name = "Baby";
6  print "Hi I'm $name in the Child Package here.\n";
7  Parent->greetme(); # Parent::greetme() will fail
}
```

(Output)
6 Hi I'm Baby in the Child Package here.
7 Hi Baby I'm your Gramps from package Grandpa.

## EXPLANATION

- 1. The package *Grandpa* is declared.
- 2. The subroutine *greetme* is defined and, when called, the *print* statement will be executed. `$Child::name` refers to the scalar `$name` in the *Child* package.
- 3. The *Parent* package is declared.
- 4. The `@ISA` array is assigned the name of the package *Grandpa*. Now if a method is called from this *Child* package and Perl can't find it, it will try the *Grandpa* package listed in the @ISA array. If you try to call a normal subroutine without method invocation, Perl won't consult the @ISA array, because it uses the @ISA array only when methods are being called. Even though the subroutines used here are not technically methods, by calling *greetme* as a class method, Perl will search the @ISA array.
- 5. The *Child* package is declared.
- 6. This line will be printed from the *Child* package.
- 7. The class method *greetme* is called in the *Parent* package. The @ISA array tells Perl to look in the *Grandpa* package if the method isn't in the *Parent* package.

### 14.4.2 $AUTOLOAD, sub AUTOLOAD, and UNIVERSAL

If a subroutine (or method) cannot be found in the current package or in the @ISA array, the *AUTOLOAD* function will be called. The *AUTOLOAD* variable is assigned the name of the missing subroutine if it is used with the *AUTOLOAD* function. Arguments passed to the undefined subroutine are stored in the *AUTOLOAD* subroutine's `@_` array. If you assign a function name to the `$AUTOLOAD` variable, that subroutine will be called if the AUTOLOAD subroutine is provided in place of the missing subroutine. If the `$AUTOLOAD` variable is used with the `AUTOLOAD` subroutine, either the method or regular subroutine syntax can be used. If all fails and Perl still can't find the subroutine, a final package (class) called UNIVERSAL is searched for the missing method. The UNIVERSAL class contains three methods that all classes inherit. They are `isa()`, `can()`, and `VERSION()` (see Table 14.2). Type at your command line prompt `perldoc UNIVERSAL` for most recent documentation.

Table 14.2 The `isa()`, `can()`, and `VERSION()` Methods

| Method | What It Does | Example |
| :----- | :----------- | :----- |
| `isa()` | Returns true if one package inherits from another. | `Salesman->isa("Employee");` |
| `can()` | Returns true if a package or any of its base classes contain a specified method. | `Salesman->can("get_dar");` |
| `VERSION()` | Used to check that the correct modules are loaded for that version number. In the example, Perl calls the UNIVERSAL method `Salesman->VERSION(6.1)`. | `package Salesman; use $VERSION=6.1;` |

## EXAMPLE 14.18

```perl
1  { package Grandpa;
2    $name = "Gramps";
3    sub greetme {
4        print "Hi $Child::name I'm your $name from package Grandpa.\n";
5    }
6  }
7
8  { package Parent;
9    sub AUTOLOAD {
10       print "$_[0]: $_[1] and $_[2]\n";
11       print "You know us after all!\n";
12       print "The unheard of subroutine is called $AUTOLOAD.\n"
13   }
14  }
15
16 { package Child;
17   $name = "Baby";
18   print "Hi I'm $name in the Child Package here.\n";
19   Parent->unknown("Mom", "Dad");   # Undefined subroutine
20 }
```

(Output):
2 Hi Baby I'm your Gramps from package Grandpa.
9 Hi I'm Baby in the Child Package here.
5 Parent: Mom and Dad
6 You know us after all!
7 The unheard of subroutine is called Parent::unknown.

## EXPLANATION

- 1 The package *Grandpa* is declared. It contains one subroutine.
- 2 This line is printed from the *Grandpa* package.
- 3 The package *Parent* is declared.
- 4 It contains an *AUTOLOAD* subroutine. An undefined subroutine is called on line 10. It has two arguments, *Mom* and *Dad*. If Perl can't find this subroutine in the *Child* package, it will look in the @ISA array, and if it is not there, Perl will look for an *AUTOLOAD* function.
- 5 The subroutine *AUTOLOAD* is defined. Since this function was called as a class method, the first argument stored in the `@_` array is the name of the class. The remaining arguments are *Mom* and *Dad*.
- 6 This line is printed to show that we got here.
- 7 The `$AUTOLOAD` variable contains the name of the class and the unnamed subroutine.
- 8 The package *Child* is declared.
- 9 This line is printed to show in what order the lines are executed.
- 10 The *Child* package wants to access a method in the *Parent* package. The *Parent* package does not contain a method or subroutine called *unknown*. It does, on the other hand, contain an *AUTOLOAD* subroutine that will be executed because this subroutine can't be found.

## EXAMPLE 14.19

```perl
1 { package Grandpa;
   $name = "Gramps";
   sub greetme {
       print "Hi $Child::name I'm your $name from package Grandpa.\n";
   }
2 { package Parent;
   # This package is empty
3 }{ package Child;
   $name = "Baby";
5 print "Hi I'm $name in the Child Package here.\n";
6 Parent->greetme();
}

7 package UNIVERSAL;
8 sub AUTOLOAD {
9   print "The UNIVERSAL lookup package.\n";
10  Grandpa->greetme();
}
```

(Output)

2 Hi I'm Baby in the Child Package here.

9 The UNIVERSAL lookup package.

5 Hi Baby I'm your Gramps from package Grandpa.

## EXPLANATION

- 1 The package *Grandpa* is declared.
- 2 The subroutine *greetme* is defined in this package.
- 3 The package *Parent* is declared. It is empty.
- 4 The package *Child* is declared.
- 5 This line is printed to show the flow of execution in the program.
- 6 The *greetme* subroutine is called as one of the *Parent* package methods. Since the method could not be found in its own class or in the @ISA array, and an *AUTOLOAD* function is not supplied in the *Parent* package, Perl looks for package *UNIVERSAL* as a last resort.
- 7 This is the built-in base called *UNIVERSAL*. All modules inherit from *UNIVERSAL* which is implicitly on the end of the @ISA array.
- 8 The *AUTOLOAD* function will automatically be called from the *UNIVERSAL* class.
- 9, 10 Within the *AUTOLOAD* function, the *greetme* function in the *Grandpa* package will be invoked.

### 14.4.3 Derived Classes

As already discussed, inheritance is when one class can inherit methods from an existing class. The existing class is called the base, parent, or superclass, and the new class that inherits from it is called the derived, child, or subclass. The base class has capabilities that all its derived classes inherit, and the derived classes can go beyond these capabilities.

If a derived class inherits from one base class, it is called single inheritance. For example, single inheritance in real life might be that a child inherits his ability to draw from his father. If a derived or subclass inherits from more than one base class, this is called multiple inheritance. To continue the analogy, the child inherits his ability to draw from his father and his ability to sing from his mother. In Perl, the derived class inherits methods from its base class and can add and modify these methods when necessary.

The classes are inherited by putting them in the @ISA array. In Chapter 13, "Modularize It, Package It, and Send It to the Library!" we looked at modules from the Perl standard library and modules you could create yourself. In order to include a module or pragma into your program, the `use` function was called with the module name (minus the .pm extension). The module had the capability of exporting symbols to other packages that might need to use the module. A special module called `Exporter.pm` handled the details for exporting and importing symbols between modules and the symbols were listed in the @EXPORT and @EXPORT_OK arrays. The `Exporter.pm` module, you may recall, was listed in the @ISA array in order to inherit methods necessary for it to do its job. But if a module functions as a class, then its methods can be called without using `Exporter`. Note in the following examples, the class methods and the instance methods are not exported.

The following examples demonstrate inheritance. The user program need not make any reference to the base class, *Employee*. The *Salesman* class and the *Teacher* class are derived from *Employee*. The *Salesman* and *Teacher* class "use" the *Employee* class. Figure 14.5 shows this inheritance hierarchy graphically.
