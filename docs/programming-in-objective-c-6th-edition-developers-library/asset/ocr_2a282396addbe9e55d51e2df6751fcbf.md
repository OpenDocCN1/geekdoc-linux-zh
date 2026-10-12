```
1 2 e
N 1
i 3
```

Note that the value displayed for K can be anything because its value was not set by the S call and it was not initialized by the program.

The statements
Click here to view code image
#
#

are analyzed by the preprocessor. If the identifier D          has been previously d          (# D       ), the preprocessor sends the statements that follow up to the @s          (the two f  c        ) to the compiler to be compiled. If D          hasn’t been defined, the two f  c        s never make it to the compiler (they’re removed from the program by the preprocessor). As you can see, the program prints out messages after it reads in the integers. The second time the program is run, an invalid character is entered (@s). The debugging output informs you of the error. Note that to turn off the debugging code, all you have to do is remove (or comment out) the line
#

and the f          statements are not compiled with the rest of the program. Although this program is so short you might not feel it’s worth the bother, consider how easy it is to turn debugging code on and off in a program several hundreds of lines long by simply changing one line.
You can even control the debugging from the command line when the program is compiled. If you’re using g  , the command
s

compiles the file d       , defining the preprocessor variable D        for you. This is equivalent to putting the following line in your program:
#

Take a look at a slightly longer program. Program 17.2 takes up to two command-line arguments. Each of these is converted into an integer value and is assigned to the corresponding variables a and a . To convert the command-line arguments into integers, the standard library function a   is used. This function takes a character string as its argument and returns its corresponding representation as an integer. The a          function is declared in the header file <       , which is included at the beginning of Program 17.2.

After processing the arguments, the program calls the p          function, passing the two command-line values as arguments. This function simply returns the product of these two arguments. As you can see, when the D      identifier is defined, various debugging messages are printed, and when it isn’t defined, only the result is printed.

# Program 17.2 Compiling in Debug Code

Click here to view code image