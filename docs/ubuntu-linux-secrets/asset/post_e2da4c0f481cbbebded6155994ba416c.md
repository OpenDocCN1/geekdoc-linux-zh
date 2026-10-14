
![](img/39e65eeb4f54001ede08c6114ae3cc6c_733_0.png)

Figure 28-2: The main NetBeans window.

2. Select File → New Project to start a new project. The New Project window, shown in Figure 28-3, appears.

![](img/39e65eeb4f54001ede08c6114ae3cc6c_733_1.png)

Figure 28-3: The New Project window.

3. Click the Next button to start a new application project. The New Project Application window, shown in Figure 28-4 appears. Enter the project name (shown as Factorial in the figure) and click the Finish button.

![](img/39e65eeb4f54001ede08c6114ae3cc6c_734_0.png)

Figure 28-4: The New Project Application window.

The NetBeans interface automatically creates the main Java code file for the application and generates the class code required.

4. Enter your application code in the main method section. The code view window appears for the Main.java code file, which contains the main class method for the application. Scroll down to the main method, and enter the following code:

```
int number = (int)(Math.random() * 10);
int factorial = 1;
int counter;

for(counter = 1; counter <= number; counter++)
{
    factorial = factorial * counter;
}
System.out.println("The factorial of "
    + number
    + " is "
    + factorial);
```

As you type the code, notice that NetBeans automatically color-codes the program text. Color coding helps you pick up any typos or coding goofs before compiling the program. Also, pause for a little bit as you type the period after the Math class. NetBeans automatically brings up a list of all the methods available in the Math

class, allowing you to pick the one you need! The completed code should look like the code in Figure 28-5.

![](img/39e65eeb4f54001ede08c6114ae3cc6c_735_0.png)

Figure 28-5: The Factorial class code.

- 5. Save the file, and build the new code by selecting the Build Main Project icon (the hammer) on the toolbar.

- 6. Run the code by selecting the Run Main Project icon (the green arrow) on the toolbar.

When the application runs, NetBeans opens a text output window at the bottom of the NetBeans window to display the program output.

NetBeans also provides a complete debugging feature, allowing you to set breakpoints in the code by simply clicking in the left margin next to the code line. To start the debugger, all you need to do is click the Debug Main Project icon (the list with the green arrow) on the toolbar.

> Secret
> 
> Once you've completed your project, NetBeans creates a jar file containing all of the class files required for your application. To find the jar file, though, you'll need to do some digging. If you used the default locations for the project, the Factorial jar file will be located in the NetBeansProjects folder in your home folder, under the Factorial folder, in a folder called dist.
> 
> To run the Factorial class from this jar file, you can use the -jar option of the Java program:

```
rich@testbox:~/NetBeansProjects/Factorial/dist$ java -jar Factorial.jar
The factorial of 3 is 6
rich@testbox:~/NetBeansProjects/Factorial/dist$
```

## Eclipse

The Eclipse IDE is an open-source graphical environment for creating and troubleshooting different types of program code, including Java code. Because of its versatility, installing Eclipse requires a couple of different software packages. Fortunately, the Synaptic Package Manager can take care of that for us.

Just start the Synaptic Package Manager (by selecting System Administration Synaptic Package Manager), then search for the eclipse-jdt package. Mark that package for installation, and Synaptic automatically installs everything that's required to develop Java applications (including the OpenJDK package, if it's not already installed).

The Eclipse package is not supported by Canonical, so it doesn't appear in the standard Ubuntu repositories. You must ensure you have the universe repository selected in your Synaptic Package Manager configuration to download the Eclipse package.

To do that, start the Synaptic Package Manager, then select Settings from the menu. In the Ubuntu Software tab section, ensure that the community-maintained, open-source software (universe) check box is selected. Then click the Reload toolbar button on the main page to reload the repository library information.

Once you install the Eclipse package it appears in the Programming menu area as well. Follow these steps to create a Java application using the Eclipse IDE:

- 1. Start the Eclipse IDE package. Select Applications Programming Eclipse from the Panel menu. The Eclipse main window, shown in Figure 28-6 appears.

![](img/39e65eeb4f54001ede08c6114ae3cc6c_736_0.png)

Figure 28-6: The Eclipse IDE main window.
