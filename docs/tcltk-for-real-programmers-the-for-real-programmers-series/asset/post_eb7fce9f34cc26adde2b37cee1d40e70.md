
## 7.1 Namespaces and Scoping Rules

A namespace can be populated with procedures and data either in a single namespace eval command or in multiple invocations of the namespace eval command.

The following example shows a namespace procedure that provides a unique number by incrementing a counter. The counter variable, staticVar, is maintained within the uniqueNumber namespace. The getUnique procedure, which is also defined within the uniqueNumber namespace, can access this variable easily, but code outside the uniqueNumber namespace cannot.

### Example 7.1.6-1

```cl
Example Script
#
# Create a namespace.
namespace eval uniqueNumber {
# staticVar is a variable that will be retained between
# evaluations
# This declaration defines the variable and its initial value.
variable staticVar 0;

# allow getUnique to be imported into other scopes
namespace export getUnique

# return a unique number by incrementing staticVar
proc getUnique() {
  # This declaration of staticVar is the equivalent of a
  # global - if it were not here, then a staticVar
  # in the local procedure scope would be created.
  variable staticVar;
  return incr staticVar;
}

# Display the currently visible namespaces:
```

```cl
puts "Visible namespaces from the global scope: \n \n[namespace children]\n"
```

# Chapter 7. Namespaces and Packages

# Display "**" commands that are visible in the global
# scope before import

```cl
puts "Before import, global scope contains these \"get*\" \ncommands: \n [info commands get*]"
```

# Import all exported members of the namespace uniqueNumber
namespace import ::uniqueNumber::

# Display "get*" commands that are visible in the global
# scope after importing

```cl
puts "After import, global scope contains these \"get*\" \ncommands: \n [info commands get*] \n"
```

# Run getUnique couple times to prove it works

```cl
puts "first Unique val: [getUnique]"
puts "second Unique val: [getUnique]"
```

# Display the current value of the staticVar: 

```cl
puts "staticVar: \n[namespace eval uniqueNumber {set staticVar}]"
```

# The next line generates an error condition because
# staticVar does not exist in the global scope.

```cl
puts "staticVar: $staticVar"
```

# Script Output

```
Visible namespaces from the global scope are:
:uniqueNumber
```

```
Before import, global scope has these "get*" commands:
gets
```

```
After import, global scope contains these "get*" commands:
gets getUnique
```

```
first Unique val: 1
second Unique val: 2
staticVar: 2
can't read "staticVar": no such variable
```

## 7.1 Namespaces and Scoping Rules

There are a few points to note in this example:

- The procedure getUnique can be declared as an exported name before the procedure is defined.
- After the uniqueNumber namespace is defined, there are two namespaces visible from the global scope—the ::uniqueNumber namespace and the ::tcl interpreter. The ::tcl namespace is always present when the Tcl interpreter is running.
- The namespace import ::uniqueNumber:* imports all exported entities from ::uniqueNumber into the global scope.
- The value of the staticVar variable can be accessed via the namespace eval. ::uniqueNumber::staticVar.
- The staticVar variable is initialized by the line variable staticVar 0 when the namespace is created. This code is equivalent to set staticVar 0 arguments to namespace eval, which would cause the variable to be defined at the top scope of the uniqueNumber namespace.

## 7.1.7 Namespace Nesting

If procedures in two namespaces need functionality that exists in a third namespace, there are a couple of options. They can create a shared copy of the third namespace in the scope of the first two namespaces, or each can create a copy of the third namespace nested within its own namespace scope.

One advantage of nesting the third namespace is that it creates a unique copy of the persistent data defined within the third namespace. If a namespace is shared, then that data is shared.

The next example shows the uniqueNumber namespace being nested within two separate namespaces (Package1 and Package2). This allows each procedure in Package1 and Package2 to get unique numbers with no gaps between numbers.

If the uniqueNumber namespace were created at the global level and shared by Package1 and Package2, then whenever either package called getUnique the unique number would be incremented.

### Example 7.1.7-1

```cl
# # This procedure creates a uniqueNumber namespace in the scope of
# the script that invokes it.

proc createUnique() {
    uplevel 1 {
        namespace eval uniqueNumber
        variable staticVal 0
        namespace export getUnique;
        proc getUnique() {
            variable staticVal
            return [incr staticVal]
        }
    }
}
```

# Create the Package1 namespace,
# Create a uniqueNumber namespace within the Package1 namespace
# The Package1 namespace includes a procedure to report unique
# numbers

```cl
namespace eval Package1 {
    createUnique
    namespace import uniqueNumber::*
    proc pack1demo() {
        return "pack1demoUnique.[getUnique]"
    }
}
```

# Create the Package2 namespace,
# Create a uniqueNumber namespace within the Package2 namespace
# The Package2 namespace includes a procedure to report unique
# numbers

```cl
namespace eval Package2 {
    createUnique
    namespace import uniqueNumber::getUnique
    proc pack2demo() {
        return "pack2demoUnique.[getUnique]"
    }
}
```

## 7.1 Namespaces and Scoping Rules

```cl
puts "Package1 example returns: [::Package1::pack1demo]"
puts "invoking Package1::getUnique directly returns: \n[Package1::getUnique]"
puts "Package1 example returns: [::Package1::pack1demo]"
puts ""
puts "Package2 example returns: [::Package2::pack2demo]"
puts "Package2 example returns: [::Package2::pack2demo]"
puts "Package2 example returns: [::Package2::pack2demo]"
```

# Script Output

```
Package1 example returns: pack1demoUnique.1
invoking Package1::getUnique directly returns: 2
Package1 example returns: pack1demoUnique.3
Package2 example returns: pack2demoUnique.1
Package2 example returns: pack2demoUnique.2
Package2 example returns: pack2demoUnique.3
```

Note that the createUnique process uses the uplevel to force the namespace eval to happen at the same scope as the code that invoked createUnique. By default, a procedure will be evaluated in the scope in it was defined. Since the createUnique procedure is created in the global scope, it will, by default, create the getUnique namespace as a child of the global space. By using the uplevel command, we force the evaluation to take place in the scope of the calling script; within the package namespace.

Here's what the namespaces look like the previous example has evaluated.

| Global Scope | namespace ::package1 |
| :--- | :--- |
| defines the namespace scope::package1 | defines the namespace scope::package2 |
| procedure::pack1demo is defined in this scope | procedure::pack2demo is defined in this scope |
| namespace::uniqueNumber is Included in this namespace | namespace::uniqueNumber is Included in this namespace |
| uniqueNumber::getUnique is imported | uniqueNumber::getUnique is imported |
| namespace::package1::uniqueNumber | namespace::package2::uniqueNumber |
| procedure uniqueNumber::getUnique is defined in this scope | procedure uniqueNumber::getUnique is defined in this scope |
| getUnique is exported | getUnique is exported |

## 7.2 Packages

The *namespace* command allows you to encapsulate information and procedures within a script. The package commands allow you to group a set of procedures identify them with a single name. The package command provides library functionality, while the namespace command provides encapsulation functionality.

This section will discuss how to turn a set of procedures into a package that can be automatically loaded by other scripts.

I've been calling a script with a collection of procedures and variables that work together to perform related functions. What's been developed so far in the examples isn't *really* a package in the Tcl sense, although it's close.

What's missing is the *package provide* command, which declares that this collection of procedures and variables is identified by a single identifier (the package name) and that this collection constitutes a particular revision of that package.

When a set of procedures have been identified this way, they can be indexed and loaded automatically when they are needed by a script.

The Tcl package command provides a framework for:

- Automatically loading files when a procedure defined within those files is required.
- Tracking the version numbers of packages and loading the requested version.
- Defining whether the file to be loaded is a script file (discussed here) or shared library/DLL (discussed in Chapter 12, Building Extensions).

## 7.2.1 How Packages Work

When a set of code is defined as a package, an index file is created that lists the procedures that are included in that package.

When the Tcl interpreter encounters an unrecognized command, it invokes a script that checks to see if that command is available in a known package.
