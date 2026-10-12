# **Command-line Arguments**

Many times, a program is developed that requires the user to enter a small amount of information at the terminal. This information might consist of a number indicating the triangular number that you want to have calculated or a word that you want to have looked up in a dictionary.

Rather than having the program request this type of information from the user, you can supply the information to the program at the time the program is executed. This capability is provided by what is known as *command-line arguments*.

As pointed out previously, the only distinguishing quality of the function **m** is that its name is special; it specifies where program execution is to begin. In fact, the function **m** is actually *called* upon at the start of program execution by the C system (known more formally as the *runtime* system), just as you call a function from within your own C program. When **m** completes execution, control is returned to the runtime system, which then knows that your program has completed execution.

When **m** is called by the runtime system, two arguments are actually passed to the function.

The first argument, which is called **a** by convention (for *argument count*), is an integer value that specifies the number of arguments typed on the command line. The second argument to **m** is an array of character pointers, which is called **a** by convention (for *argument vector*). There are **a** + 1 character pointers contained in this array, where **a** always has a minimum value of 0.

The first entry in this array is a pointer to the name of the program that is executing or is a pointer to a null string if the program name is not available on your system. Subsequent entries in the array point to the values that were specified in the same line as the command that initiated execution of the program. The last pointer in the **a** array, **a**, is defined to be null.

To access the command-line arguments, the **m** function must be appropriately declared as taking two arguments. The conventional declaration that is used appears as follows:

Click here to view code image

```
```
i
{
}
```
```

Remember, the declaration of **a** defines an array that contains elements of type “pointer to **c**.” As a practical use of command-line arguments, recall **Program 9.10**, which looked up a word inside a dictionary and printed its meaning. You can make use of command-line arguments so that the word whose meaning you want to find can be specified at the same time that the program is executed, as in the following command:

```
```
1
```
```

This eliminates the need for the program to prompt the user to enter a word because it is entered on the command line.

If the previous command is executed, the system automatically passes to **m** a pointer to the character string “ **in** a **. Recall that a contains a pointer to the name of the program, which in this case is “ .**”,

The **m** routine might appear as follows:

Click here to view code image