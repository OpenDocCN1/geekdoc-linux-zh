# ADD A METHOD

A method enables you to split up parts of a module or class into various subroutines, as well as create a block of code associated with a subroutine name. You can use methods to call a block of code from other methods inside the class or module. Depending on its scope, you can access the method outside of its module or class. For more information on the scope of a method, see the section "Declare a Variable."

When a block of code calls a method, the execution of that code block stops and your method begins. When VB.NET reaches the end of the code in your method, execution passes back to the code block that calls it and proceeds. However, any code you place in a separate method cannot access data from the code block that invokes it. You use arguments to give a list of required information. For more information on arguments, see the section "Pass Information Through Methods."

To create a new method inside an existing code module, you have two options. If the code does not need to pass information back to the code that calls it, you can use the Sub keyword. If the routine needs to return a value to the code that calls it, use the Function keyword. For a method defined as a Function, you must designate the return type for the Function using the As keyword along with a variable type after the parameter list. For more information on returning values, see the section "Pass Information Through Methods."

To call a method that you create in the same module or class, place the name of the method on a line of its own and follow it by a set of parentheses. If the method requires arguments, enclose the values to pass to the method inside the parentheses. You separate multiple arguments with commas.

![](bbox=[0.045, 0.5, 0.955, 0.77])

+   1. Create a new Console Application or open any existing project.
+   Note: See the section "Create a Console Application" for details.
+   2. Open the class or module to which you want to add a method in the Code Editor.

+   You can right-click a module or form in the Solution Explorer and click View Code to open a module.
+   3. Click a blank line outside of any other methods.

+   4. Type Sub AskUserName(), replacing AskUserName with the name of the method.
+   You can type the Function keyword instead of Sub to create a method that returns parameters.

+   5. Press Enter.
+   Visual Basic creates the End Sub keyword.
+   6. Type the code for your method between the Sub and End Sub.