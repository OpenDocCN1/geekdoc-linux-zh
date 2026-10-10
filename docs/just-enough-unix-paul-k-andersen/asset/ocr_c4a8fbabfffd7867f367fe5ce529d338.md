# ### 28.5 Creating and Running recip.p

1 **Create a source file.** Use the *vi* editor to create a file named $recip.p$:

```
$ vi recip.p Return

```

Enter the program exactly as shown in Listing 28-2B, then write to the file and quit the editor.

2 **Compile the source code.** The default name for an executable file is a.out. You can specify another name using *pc* with the *-o* option. For the executable file, let’s use the name *recip* (without the *.p* suffix):

```
$ pc -o recip recip.p Return

```

This tells *pc* to compile $recip.p$ and put the executable in the file $recip$.

3 **If necessary, correct any syntax errors and repeat Step 2.**

4 **Run the program.** To run the program, enter the name of the executable file:

```
$ recip Return

```

You should see a message and a prompt:

> > This program computes reciprocals.
> > Enter a number:

5 **Enter a number at the prompt.** Try the number 2:

> > Enter a number: 2 Return

The program will respond:

> > The reciprocal of 2 is 0
> > $

This is obviously wrong: the reciprocal of 2 is 1/2, not 0. In fact, $recip.p$ gives the correct answer only when you enter $-1$ or 1 as input. The reason has to do with the way that the computer stores and uses integers. To repair this defect, you should revise the program to use variables of type *real* rather than type *integer*. (We leave this as an exercise.)

# ### 28.6 Arithmetic Exceptions and Core Dumps

How does the $recip.p$ program handle division by zero?

1 **Run the program.**

```
$ recip Return

```

The program will print a message and a prompt: