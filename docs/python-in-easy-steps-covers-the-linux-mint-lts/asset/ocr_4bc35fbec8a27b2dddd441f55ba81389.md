# Storing functions

Python function definitions can, usefully, be stored in one or more separate files for easier maintenance and to allow them to be used in several programs without copying the definitions into each one. Each file storing function definitions is called a “module” and the module name is the file name without the “.py” extension.

Functions stored in the module are made available to a program using the Python import keyword followed by the module name. Although not essential, it is customary to put any import statements at the beginning of the program.

Imported functions can be called using their name dot-suffixed after the module name. For example, a “steps” function from an imported module named “ineasy” can be called with ineasy.steps().

Where functions stored in a module include arguments, it is often useful to assign a default value to the argument in the definition. This makes the function more versatile, as it becomes optional for the call to specify an argument value.

+   1 Start a new Python module by defining a function that supplies a default string value to its argument for display
+   def purr( pet = ‘A Cat’ ) :
+       print( pet , ‘Says MEOW!’ )

![](bbox=[0.11, 0.65, 0.21, 0.75])

+   2 Next, add two more function definitions that also supply default string values to their arguments for display
+   def lick( pet = ‘A Cat’ ) :
+       print( pet , ‘Drinks Milk’ )
+   def nap( pet = ‘A Cat’ ) :
+       print( pet , ‘Sleeps By The Fire’ )