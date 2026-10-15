# CREATE A CONSOLE APPLICATION

Console applications provide the most basic Visual Basic .NET program: they display textual information in a console. An example of a console window is the Command Prompt application. You can create console applications to provide a simple way to test and develop code without the additional effort necessary for visual form development. The Console object gives all the necessary methods to output information to the user and read information from the user, taking the place of forms and controls. See Chapter 2 for more information on Windows Forms applications.

The System.Console object provides the functionality to access the console. Unlike a Windows Forms-based application, a console application does not require a class and simply loads from a default module with a Sub Main procedure.

You use the Console Application project template to create a new application. Code execution always begins in the Sub Main module, but you can create supplementary classes and modules to support the application. Chapter 7 contains more information about classes.

To write a line of text to the console, use the WriteLine method of the Console object. For example, WriteLine("Test") writes Test to the console and moves to the next line. If you want to output text without moving to the next line, use the Write method. Pass a string of text enclosed in quotes or pass a variable to either of these methods to output the information. For more information on passing parameters to methods, see the section "Pass Information Through a Method."

To read a single character from the input stream, use the Read method. The Read method returns the character value as an Integer. To read in a line of information, use the ReadLine method. The ReadLine method returns a String variable. For more information on creating a string variable to hold the result, see the section "Create a String."

# CREATE A CONSOLE APPLICATION

![](bbox=[0.04, 0.6, 0.95, 0.86])

+   1. Click File > New > Project.
+   2. Click Console Application from the templates list.
+   3. Type a name for the project.
+   4. Click OK to create the project.
+   The New Project dialog box appears.
+   The project opens a default module and declares a Sub Main procedure.