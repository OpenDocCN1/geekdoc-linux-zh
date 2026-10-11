# Pretty Linux

Mr. Gates finally gave DOS a makeover, and it came out looking like Windows. Linux, however, is still undergoing its makeover. The first improvement enables a user to open more than one window on-screen. To do so, the user needs special software known as X Windows. The next improvement involves jazzing up those windows with push buttons, drop-down lists, and all

those things that Windows machines and Macs display. You need additional special software for this improvement. That software is known as Motif. So unless you intend to find out how to build your program so that you can use X Windows and Motif with it, you must live with a basic program that doesn't use the windowing features you see on Windows and Mac.

You can't write a pretty user interface for Linux like you see in Macs and PCs running Windows programs unless you know how to program X Windows and Motif (see Chapter 1). Linux is a plain-Jane operating system, like DOS. Expect your program only to wait patiently until someone presses the Enter key after typing each piece of information. In the meantime, your computer's collecting and storing all the keystrokes somewhere inside it that's known as a *keyboard buffer*. After the user presses the Enter key, your program rushes to grab all those characters that the user entered at the keyboard and stuff them into the variables that you created for them.

# Reading a string

Your computer isn't too bright whenever it must pick up data from the keyboard. (But, on the other hand, it would like to use *us* find the square root of 365 in less than a second.) Your computer doesn't know whether to treat a number as a character or a value to use in a calculation. It finds out only after you specify the kind of variable that you want to use to store the information.

After you tell the computer the correct variable to use, you must tell it to read the characters from the keyboard. The following code shows you how to tell the computer to read characters and then stuff them into a string variable:

```
#!/bin/bash
clear
echo
echo "Enter Your First Name: "
read FirstName
```

First, `#!/bin/bash` tells the computer to start the *bash* shell before clearing (clear) the screen.