# Chapter 14

# Getting Down with Subprograms

# In This Chapter

+   > Creating a program plan
+   > Creating subprograms
+   > Naming subprograms
+   > Using subprograms
+   > Sharing subprograms

Although you design each program to perform a specific task, every program that you write shares some basic functions in common with other programs. Every program, for example, displays text on a screen, reads information that a user enters on the keyboard, saves the user’s input to a variable, and then works with the information.

You piece each of these tasks together to build large, complex programs that tell the computer to perform some useful tasks. At times, you want your program to perform a specific group of related tasks, such as displaying an error message on-screen if the user does something wrong with your program.

Pretty soon, you’re writing Linux programs that enable your computer to do all sorts of fancy things.

Because errors can occur practically anywhere in your program, duplicating the necessary instructions to display an error message throughout your program doesn’t make sense. Such duplication takes up too much space and is a nightmare to maintain. Every time that you change a part of the error message, you must remember all the places in your program where you duplicate those instructions.

You can avoid the problems that result from duplicate instructions in your program simply by placing those instructions in a small program known as a subprogram. A subprogram is identical to a regular program in that you create a subprogram by using an editor and the chmod command to transform the file into an executable program (a file that your computer can run).