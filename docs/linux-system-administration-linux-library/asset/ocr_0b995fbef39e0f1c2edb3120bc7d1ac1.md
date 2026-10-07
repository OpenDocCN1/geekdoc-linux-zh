# Control Statements

Because scripts (and programs generally) usually do repetitive work, it's necessary that languages include some means of directing the flow of a program. For instance, if you write a script to search every file in a directory for certain characteristics, you need some way to tell the program to jump to another part of itself—say, to skip instructions that aren't relevant to a particular file, because it doesn't meet certain criteria. These tasks are handled by what are are collectively known as *control statements*. These statements control the flow of the program.

There are several types of control statements, although some are more important than others, and some languages discourage the use of some statements. The major types are:

**Conditional** A conditional expression tells the program to do one thing if a particular condition is met, and to do another if condition is not met. (There are also conditionals that support more than two options.) For instance, you might use a *conditional* if you want to copy all files whose names begin with a a. Your conditional statement would execute one of operations if the filename begins with a a and another if it doesn't.

**Loops** A loop allows the program to perform the same task repeatedly, usually on different data. For instance, you might use a loop to examine all the files in a directory. The loop would execute once of for each file, and then terminate.

**Subroutines** A subroutine isn't a control statement *per*, but it is an important aspect of many programming languages. A subroutine isolates a segment of code to perform a specific task. The main program can then execute the subroutine, often as if it were a simpler command. For instance, you might write a subroutine to calculate a circle's circumference given its diameter, and then call it when you need this computation.

**Jumps** A jump sends execution of the program to another point. Jumps can be used to implement loops and subroutines, but they're generally frowned upon by today's programmers because they can produce a tangled mess of program, in which it's difficult to determine the sequence of execution (often referred to as spaghetti code).

It's possible—and often necessary—to combine two or more of these types of control statements to perform a task. For instance, a loop might contain one or more conditionals, in order to take different actions depending on the type of data stored in the variables loop examines. Most loops actually incorporate conditional-style logic to control termination. That is, the loop executes until some condition is met, such as reaching the end of a set of inputs.