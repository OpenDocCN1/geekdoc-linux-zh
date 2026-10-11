Add together the numbers for each permission level that you want to grant yourself (4 + 2 + 1 = 7). The sum, 7, is the first of the three numbers that you use with the `chmod` utility. If you just want to grant yourself read and write permissions without making the file an executable file, however, you use the number 6 (4 + 2 = 6) with the `chmod` utility for your own level of permission.

So `chmod 711 myfile` (where `myfile` is the name of the file to which you're assigning permissions) means that the owner (you) has read, write, and executable permissions and that both the group and others can only execute your program.

# Linux Shell-Script Languages versus Other Languages

Because writing a program in Linux requires a different way of thinking than does programming in other computer languages, this section gives you some important features that are easy to overlook. They're here, at your fingertips, whenever you feel a lapse of memory coming on.

# Linux utilities already exist

In most programming languages, you first plan what you want the computer to do and then decide which instructions to give it to make that happen. Linux programming is a little different. You still must plan the task to get the job done, but most of the instructions already exist in the form of a Linux utility. So you need only to divide your program into the tasks that you want the computer to perform and then find the appropriate Linux utility to carry them out. (Bell Labs created Unix so that programmers can quickly assemble their programs from well-tested utilities. All you need to do is to choose the right utilities and put them in your program.)

Each utility requires input (that you supply). After the utility finishes working, it delivers output that you can use as input for another utility. As an example, a text-editor utility creates a file that you can use as input for the spell-check utility.

Learning how to use a Linux utility could become a nightmare if not for this clever little trick: Most utilities include a how-to manual, known as a `man page`, that's installed on any computer running Linux. (And, no, it's not a list of eligible men.) `Man` is short for `manual`. To display the manual on-screen, just type the following line (replacing `utility` with the utility name) and press `Enter`:

```
```bash
man utility
```
```