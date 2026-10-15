
## INHERIT A FORM

Because a Form in VB .NET is nothing more than a class, you can inherit a form into a new form using standard inheritance techniques. You can use visual inheritance of forms to create base forms that encourage uniform appearances and easier management. For example, a base form can represent the appropriate size and button placements for the dialogs in the application. Each dialog in the application inherits this base form and builds the interface necessary for the particular dialog, but maintains the same size and button functionality of the base form.

The Windows Forms Designer supports inheritance for forms. On the designer, inherited controls appear with a small icon over them to indicate that they inherit from the base class. You can change properties of the inherited items, but cannot delete them because the base class predefines them. See the section "Inherit from Existing Classes" for more information on inheriting classes.

All of the event handlers you specify in the base form automatically work the same in the inherited form. If a button on the base form specifies an event handler, the inherited form's button calls the event handler in the base class. If you add an event handler in the inherited class for a component on the base class, both event handlers fire. The base class's event handler fires first, followed by the inherited class's event handler.

You can override an event handler in the base form, however. To accomplish this, place the Overridable keyword in the definition of the base class's event handler, and then create a new method in the inherited class with the same parameter list. Do not place the Handles keyword on the inherited form's override method. If you want to call the base form's event handler inside the overridden method, use the MyBase object to access the base form.

## INHERIT A FORM

![](img/d6f772854306e15fb6df39b861a7b541_209_0.png)

- 1. Create a new form or open an existing one to act as the base class adding controls as necessary.
- Note: See Chapter 1 to build a project.
- 2. Build the project.
- Note: See Chapter 2 to build a project.
- 3. Click Project -> Add Inherited Form.
- 4. Type a name for the inherited form.
- 5. Click Open.

## Extra

Remember that the inheritance of a form is not a one-time operation. Although you inherited from a base form in a particular state, you can always change the base form to add functionality. For example, you can update the base form to replace old controls with new ones that have the same function but a more attractive appearance. Likewise, you can debug the code in the base form and have it automatically update all of the inherited forms. To alter the base form, make sure you close all inherited forms. You then open the base form, make changes, and rebuild the project. When you reopen inherited forms, you see your changes.

When using inheritance on forms, you do not need to inherit controls. You can create a base form that declares useful variables and methods so you do not need to replicate them in each form you create. You can build a very powerful base form that makes programming additional forms quite simple. Make sure to add the Overridable keyword, when appropriate, to allow inherited forms to extend the functionality.

![](img/d6f772854306e15fb6df39b861a7b541_210_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_210_1.png)

6 Select the form you created in step 1 to act as the base form.

The Inheritance Picker dialog appears.

7 Click OK.

VB .NET creates the inherited form.

You can now modify and extend the form using standard visual design techniques.

Note: See Chapter 8 to learn how to override methods. See Chapter 3 to modify, add controls, and manipulate the form.

## CREATE A THREAD

Threads enable multiple parts of your application to execute concurrently. You can use threads to start a calculation or network connection without affecting the usability of the program. For example, when your application performs a search of the file system for the user, you do not want to force the user to stop working in another part of your application while waiting for the search to complete. Instead, you can create a thread to complete the search that runs concurrently with the rest of your application.

Threading in VB.NET operates using a free-threaded system. With free-threading, all threads run in the same memory space in the application. This means you can access all variables, objects, and components available in the program through the thread. Before you create a thread, understand that many complexities arise when multiple parts of code access variables and objects concurrently. See the section "Write Thread-Safe Code" for more information on Visual Basic .NET's synchronization commands.

In VB.NET, a thread runs the code of a single method in a separate thread. The method can call other methods in its thread. To create a new thread, you create a new instance of the Thread class. The System.Threading namespace contains the Thread class. You pass the address of a method to run using the AddressOf keyword. For more information on using AddressOf, see the section "Using Delegate and AddressOf".

To start the thread, call its Start method with no parameters. The thread runs until it meets one of three conditions. The thread stops when the code in the method completes, when the process containing the thread ends (normally meaning your program exits), or when you stop the execution explicitly. See the section "Modify Thread Execution" for more information.

The Thread.CurrentThread method returns the currently running thread. You can use this method anywhere, which makes it easy to receive an instance of the thread you create.

## CREATE A THREAD

![](img/d6f772854306e15fb6df39b861a7b541_211_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_211_1.png)

- 1. Create a new project or open an existing one.
The example uses a console project.
- 2. Add a method to a code module for the thread to run.
Note: See Chapter 4 for more information on console applications.
- 3. Type Dim followed by a variable name.
- 4. Type As New System.Threading.Thread ().
- 5. Inside parentheses, type AddressOf followed by the name of the method.
The example loads the thread in Sub Main.
