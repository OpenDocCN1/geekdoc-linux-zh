The following steps describe what happens as I run this program:

+   1. Linux sees the first line `#!/bin/bash` and knows to run the *bash* shell.
+   2. Then Linux substitutes the `$1` with the command-line argument `bob@mycomputer`. This argument is, of course, the destination address.
+   3. Finally, Linux runs the *mail* utility that sends the message that the `$memo1` file contains to `bob@mycomputer` with the subject of *Good News*.

# Passing the copy address

You pass the copy address to the e-mail program by using basically the same method that you use to pass the destination address to the program. The copy address is the e-mail address of the person who’s going to receive a copy of the e-mail that you send to the destination address.

Follow these steps to modify the e-mail program:

+   1. Start *vi* and load the program, as I show you in the section “Passing the destination address,” earlier in this chapter.
+   2. Next, change the program to look like the following example:

```
```
#!/bin/bash
mail -s "Good News" bob@mycomputer -c $1 < memo
```
```

+   3. Save the program by using the Shift+*zz* key combination (and remember that the program is already executable from the last time you saved it).
+   4. Call the program and include the copy address on the command line as shown in the following example:

```
``` 
mail program mary@mycomputer 
```
```

The following steps describe what happens next:

+   1. Linux runs the *bash* shell because you enter `#!/bin/bash` on the first line of the program.
+   2. Next, Linux substitutes `mary@mycomputer` for the `$1` (because you’re sending Mary a copy of the e-mail).

Remember that `$1` represents the information that is passed to your program from the command line. You must place the `$1` inside your program where the information passed from the command line is used if