# CREATE A SHARED METHOD

Because some methods need to function more like global procedures throughout a project, you may want to call methods inside classes without first creating an instance of the class. For example, if you create a class of mathematic routines, you do not want to declare a new instance of your class every time you need to perform a simple routine. Or, if you declare a class File and want to expose a method called Open, you can let the user call Open, which opens the file and then actually returns an instance of the File class without first having to create an instance of the File class. You can use shared methods to let a module invoke a method in a class without first creating an instance of the class.

To create a shared method, you use the Shared keyword in front of the Sub or Function keyword in the declaration of the method. When you place the keyword in front of the method, you can still use it as a normal method if you create a class instance. But you can also access the method by placing the name of the class, not a variable name of an instance of the class, in any other method that can access the class followed by a period and the name of the method.

When VB.NET runs the code, it runs the shared method just like a method in a code module. The method has no attachment to the class when run as a shared method, and therefore cannot access member variables or other class members inside the class. A shared method can only access a shared variable or shared event. For more information on shared member variables, see "Create a Shared Variable." See "Using Delegate and AddressOf" for information on the AddressOf statement.

![](bbox=[0.03, 0.48, 0.99, 0.85])

+   1. Create a new class or open an existing one.
+   2. Type an accessibility keyword on an empty line in the class.
+   3. Type Shared followed by Sub or Function.
+   4. Type a name for the method.
+   5. Type a parameter list inside parentheses.
+   6. For a Function, type As followed by a type.
+   7. Press Enter.