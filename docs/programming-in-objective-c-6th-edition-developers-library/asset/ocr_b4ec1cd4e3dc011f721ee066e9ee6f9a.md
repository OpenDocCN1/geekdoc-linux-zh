Another common application for function pointers is to create what is known as *dispatch* tables. You can’t store functions themselves inside the elements of an array. However, it is valid to store function *pointers* inside an array. Given this, you can create tables that contain pointers to functions to be called. For example, you might create a table for processing different commands that will be entered by a user. Each entry in the table could contain both the command name and a pointer to a function to call to process that particular command. Now, whenever the user enters a command, you can look up the command inside the table and invoke the corresponding function to handle it.

# **Pointers and Memory Addresses**

Before ending this discussion of pointers in C, you should note the details of how they are actually implemented. A computer’s memory can be conceptualized as a sequential collection of storage cells. Each cell of the computer’s memory has a number, called an *address*, associated with it. Typically, the first address of a computer’s memory is numbered 0. On most computer systems, a “cell” is called a *byte*.

The computer uses memory for storing the instructions of your computer program, and also for storing the values of the variables that are associated with a program. So, if you declare a variable called c to be of type int, the system assigns location(s) in memory to hold the value of c while the program is executing. This location might be at address 500, for example, inside the computer’s memory.

Luckily, one of the advantages of higher-level programming languages such as C is that you don’t need to concern yourself with the particular memory addresses that are assigned to variables—they are automatically handled by the system. However, the knowledge that a unique memory address is associated with each variable will help you to understand the way pointers operate.

When you apply the address operator to a variable in C, the value that is generated is the actual address of that variable inside the computer’s memory. (Obviously, this is where the address operator gets its name.) So, the statement

```
i
```

assigns to i the address in the computer’s memory that has been assigned to the variable c. So, if c is located at address 500 and contains the value 1, this statement assigns the value 5 to i, as depicted in *Figure 10.11*.

![](bbox=[0.25, 0.69, 0.75, 0.85])

The address of i is shown in *Figure 10.11* as I because its actual value is irrelevant for this example.

Applying the indirection operator to a pointer variable, as in the expression

```
*
```

has the effect of treating the value contained in the pointer variable as a memory address. The value