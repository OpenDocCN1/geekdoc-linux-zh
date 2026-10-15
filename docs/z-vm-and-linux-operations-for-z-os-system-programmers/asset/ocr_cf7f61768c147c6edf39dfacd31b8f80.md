To move a block of lines, enter the double character MM in the prefix area of both the first and last lines to be moved. The first and last lines to be moved, and the destination line, can all be on different screens. You can use PF selections to scroll the screen before pressing Enter.

z/OS analogy: In z/OS (ISPF editor), the M(ove) command is identical, but line command A(fter) is used instead of F(ollowing), and B(efore) instead of P(receeding).

# Copying lines

The procedure for copying lines is the same as for moving lines, except that you enter a C or CC prefix subcommand instead of M or MM. The copy operation leaves the original lines in place but makes a copy at the destination line, which is indicated by F or P.

z/OS analogy: In z/OS (ISPF editor), the C(opy) command is identical, with the same exceptions as stated for the M(ove) command previously

# Canceling prefix subcommands

If you entered one or more prefix subcommands that created a pending status, you can cancel all of them by entering the following subcommand on the command line:

```
====> reset
```

After you press Enter, all prefix subcommands disappear from the display and the prefix areas are restored with equal signs, numbers, or blank characters, depending on your particular XEDIT configuration.

If you have typed any prefix subcommands (even those that do not cause a pending status) but have not yet pressed Enter, you can clear your screen to remove them. If you have only typed a few characters, it is also be sufficient to simply type over them with blank characters.

# Moving through a file

XEDIT lets you move backward, forward, up, down, and to the top and bottom in a file. You have already seen that the PF7 and PF8 selections are set to the BACKWARD and FORWARD subcommands, which scroll one full window backward or forward. You may also enter the BACKWARD and FORWARD subcommands in the command line. The format of these subcommands is:

```
BAckwardn
FOrwardn
```