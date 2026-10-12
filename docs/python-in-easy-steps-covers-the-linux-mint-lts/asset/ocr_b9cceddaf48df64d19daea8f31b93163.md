# ## Owing function names

Internally, each Python module and program has its own “symbol table” that is used by all functions defined in that context only. This avoids possible conflicts with functions of the same name in another module if both modules were imported into one program.

When you import a module with an **import** statement, that module’s symbol table does not get added to the program’s symbol table – only the module’s name gets added. That is why you need to call the module’s functions using their module name prefix. Importing a “steps” function from a module named “ineasy” and another “steps” function from a module named “dance” means they can be called without conflict as `ineasy.steps()` and `dance.steps()`.

Generally, it is preferable to avoid conflicts by importing the module name and calling its functions with the module name prefix, but you can import individual function names instead with a **from import** statement. The module name is specified after the **from** keyword, and functions to import are specified as a comma-separated list after the **import** keyword. Alternatively, the * * wildcard character can be specified after **import** to import all function names into the program’s own symbol table. This means the functions can be called without a module name prefix.

+   1. Start a new Python module by defining a function that supplies a default string value to its argument
+      ```python
+      def bark(pet = 'A Dog'):
+          print(pet, 'Says WOOF!')
+      ```

![](bbox=[0.12, 0.71, 0.22, 0.82])

+   2. Next, add two more function definitions that also supply default string values to their arguments
+      ```python
+      def lick(pet = 'A Dog'):
+      ```