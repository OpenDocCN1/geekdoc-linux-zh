you typed it into the program. In this example, you place the $1 in the position where the copy address belongs in the instruction that calls the mail utility.

+   3. Finally, Linux calls the mail utility and sends the message that the mem01 file contains to bob@mycomputer and the mary@mycomputer copy address with the subject of Good News.

# Passing the blind-copy address

The blind-copy address tells the mail utility to send a copy of the e-mail to this address without informing anyone else that the recipient at the blind- copy address is receiving a copy. (Flip through Chapter 20 to find out more about how the blind-copy address works.)

You can pass the blind-copy address to the program by making the blind- copy address a command-line value similar to the destination and copy address that I mention in the two preceding sections. Just follow these steps:

+   1. Load the mail program into vi so that you can modify the program.

+   2. Change the mail program to look as follows:

```
```bash
#!/bin/bash
mail -s "Good News" bob@mycomputer -b $1 < mem01
```
```

+   3. Save the program.

+   4. Start the program by typing the program's name at the command prompt, making sure that you include the blind-copy address, as shown here:

```
```bash
mailprogram boss@mycomputer
```
```

> **Note:** If you're using the program from the section “Passing the copy address,” earlier in this chapter, you can just save the program because it's already executable.

The following describes what's going on in these steps:

+   1. Linux follows your directions and runs the bash shell (#!/bin/bash).

+   2. Linux then substitutes boss@mycomputer for the $1. (The boss is receiving a blind copy of the e-mail.)

+   3. Finally, Linux calls the mail utility to send mem01 message to bob@mycomputer and to the boss@mycomputer blind-copy address with the subject of Good News.