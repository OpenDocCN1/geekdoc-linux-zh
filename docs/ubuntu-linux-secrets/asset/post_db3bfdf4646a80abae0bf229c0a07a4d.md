
## Part 5: Programming in Ubuntu

on inside the program as the program runs. To properly debug a Java application, you need to compile it using the -g option. You can then start the class file in the debugger:

```
$ javac -g MyTestClass.java
$ jdb MyTestClass
Initializing jdb...
>
```

The jdb debugger is now ready for action. There are several commands you can use to control the operation of the debugger, shown in Table 28-4.

**Table 28-4: The jdb Debugger Commands**

| Command | Description |
|---|---|
| `connectors` | List available connectors and transports in the JVM |
| `run` | Start execution of the main class |
| `threads` | List the threads |
| `thread` | Set the default thread |
| `suspend` | Suspend the specified thread ID |
| `resume` | Resume the specified thread ID |
| `where` | Dump the specified thread’s stack |
| `wherei` | Dump the specified thread’s stack with pc info |
| `up` | Move up a thread’s stack |
| `down` | Move down a thread’s stack |
| `kill` | Kill the specified thread |
| `interrupt` | Interrupt the specified thread |
| `print` | Display the value of the specified expression |
| `dump` | Display all object information |
| `eval` | Evaluate the specified expression |
| `set` | Assign a new value to a variable |
| `locals` | Display all local variables |
| `classes` | List currently known classes |
| `class` | Display details of the specified class |
| `methods` | Display the methods of the specified class |
| `fields` | Display the fields of the specified class |
| `threadgroups` | List the thread groups |
| `threadgroup` | Set the current thread group to the specified thread group |
| `stop in` | Set a breakpoint at the specified class method or line |

As you can see, there are many commands you can use to examine your running Java application. Here’s a small example of starting the debugger with the sample Java code and setting a breakpoint to stop the program:

```
$ jdb MyTestClass
Initializing jdb...
> stop in MyTestClass.main
Deferring breakpoint MyTestClass.main.
It will be set after the class is loaded.
> run
run MyTestClass
Set uncaught java.lang.Throwable
Set deferred uncaught java.lang.Throwable

VM Started: > Set deferred breakpoint MyTestClass.main

Breakpoint hit: "thread-main,", MyTestClass.main(), line=3 bc1=0
3 int number = 5;

main[1]
```

After starting the debugger, I used the stop in command to set a breakpoint at the main method in the MyTestClass class. After setting the breakpoint, I used the run command to execute the program.

The debugger started the program, then stopped at the first line in the main method. At this point you can use the list command to display where in the code you are:

```
main[1] list
1 class MyTestClass {
2 public static void main(String[] arg) {
3 -> int number = (int)(Math.random() * 10);
4 int factorial = 1;
5 int counter;
6 for(counter = 1; counter <= number; counter++) {
7 factorial = factorial * counter;
8 }
9 System.out.println("The factorial of "
10 + number
main[1]
```

The debugger knows the source code and indicates the line in the source code the program stopped. You can then step through the code one line at a time using the step command, then examine variable values using the print command:

```
main[1] step
>
Step completed: "thread-main,", MyTestClass.main(), line=4 bc1=2
4 int factorial = 1;

main[1] step
>
Step completed: "thread-main,", MyTestClass.main(), line=6 bc1=4
6 for(counter = 1; counter <= number; counter++) {
```

```
main[] print number
number - 5
main[]
```

You can step through the for loop and watch the factorial variable value change in each iteration. At the end of the for loop, the factorial value will contain the final value:

```
main[] step
> 
Step completed: "thread-main", MyTestClass.main(), line=9 bci=21
9 System.out.println("The factorial of "
```

```
main[] print factorial
factorial = 120
main[]
```

You can release the program to finish by using the cont command:

```
main[] cont
The factorial of 5 is 120
> 
The application exited
$
```

After the program completes, the debugger automatically exits and returns you to the command line prompt. The debugger is a great tool to have available to troubleshoot your Java programs.

> Most graphical IDE packages provide a graphical debugging environment, which is what makes them easier to use than the command-line jdb debugger. If you have access to a graphical IDE package to develop your Java applications, you should use the debugger in that software rather than the jdb program. However, if you're in a command-line environment (such as the Ubuntu server) and need to debug a Java application, jdb can be a lifesaver!

## The jar Program

One disadvantage to Java is that you often have multiple .class files as a result of compiling separate Java programs for a single application. Distributing an application that requires multiple class files can be a problem.

To solve this problem, Java uses the jar program. The jar program creates a single library file that contains all of the class files required for an application.

The format of the jar program changes, depending on the function you're trying to perform. To create a new jar file, you'd use the format:

```
$ jar cf myjar.jar MyTestClass.class
```

This command adds the class file MyTestClass.class into a jar file called myjar.jar. If you need to add multiple files to the jar file, just add them to the command line. You can also update an existing jar file using the uf parameter. For example, if you had another
