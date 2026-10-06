
# The Linux Command Line

- Reverse video (black characters on white background)
- Blinking
- Combinations of all of the above features

Back in the old days, if you wanted to get someone's attention, you used bold, blinking, reverse video text. Now there's something that could hurt your eyes!

As color terminals became available, programmers added special control codes to display text in various colors and shades. The ANSI character set includes control codes for specifying specific colors for both foreground text and the background color displayed on the monitor. Most terminal emulators support the ANSI control codes.

# The keyboard

There is more to a terminal than just how the monitor operates. If you have ever worked with different types of dumb terminals, I'm sure you have seen that they contain different keys on the keyboard. Trying to emulate specific keys on a specific dumb terminal proven to be a difficult task for terminal emulation packages.

It was impossible for the creators of the PC keyboard to include keys for every possible type of special key in dumb terminals. Some PC manufacturers experimented with including special keys for special functions, but eventually the PC keyboard keys became standardized.

For a terminal emulation package to completely emulate a specific dumb terminal, it must remap any dumb terminal keys that don't appear on the PC keyboard. This remapping feature can often become confusing, especially when different systems use different control codes for the key.

Some special keys you'll see in terminal emulation packages are:

- BREAK: Sends a stream of zeroes to the host. This is often used to interrupt the currently executing program in the shell.
- SCROLL LOCK: Also called no scroll, this stops the output on the display. Some terminals included memory to hold the contents of the display so the user could scroll backward through previously viewed information while the scroll lock was enabled.
- Repeat: When held down with another key, this caused the terminal to repeatedly send the other key's value to the host.
- Return: Commonly used to send a carriage return character to the host. Most often used to signify the end of a command for the host to process (now called Enter on PC keyboards).
- Delete: While basically a simple feature, the Delete key causes grief for terminal emulation packages. Some terminals delete the character at the current cursor location, while others delete the preceding character. To resolve this dilemma, PC keyboards include two delete keys, Backspace and Delete.
- Arrow keys: Commonly used to position the cursor at a specific place; for example, when scrolling through a listing.
- Function keys: A combination of specialty keys that can be assigned unique values in programs similar to the PC F1 through F12 keys. The DEC vert of terminals actually had two of function keys, F1 through F20, and PF1 through PF4.

Keyboard emulation is a crucial element in a terminal emulation package. Unfortunately, often applications are written requiring users to hit specific keys for specific functions. I've seen many communications package that used the old DEC PF1 through PF4 keys, which are often a hard to find on a terminal emulation keyboard.

# The terminfo Database

Now that you have a terminal emulation package that can emulate different types of terminals, you need a way for the Linux system to know exactly what terminal you're emulate. The Linux system needs to know what controls to use when communicating with the terminal emulator. This is by using an environment variable (see Chapter 5) and a special set of files collectively called the terminfo database.

The terminfo database is a set of files that identify the characteristics of various terminals that can be used on the Linux. The Linux systems store the terminfo data for each terminal type as a separate file in the terminfo database directory. The location of this terminfo often varies from distribution to distribution. Some common locations are /usr/share/terinfo, /etc/terminfo, and /lib/terminfo.

To help with organization (often there are lots of different terminfo files), you will see that the terminfo database contains directories for different letters of the alphabet. The individual files for specific terminals are stored under the appropriate directory for their terminal name.

An individual terminfo file is a binary file that is the result of compiling a file. This text file contains codes that define function screens, associated with the code required to implement the function on the terminal.

Since the terminfo database files are binary, you cannot see the codes within these files. However, you can use the infocmp command to convert the binary entries into text. An example of using this command is:

```
$ infocmp vt100
# Reconstructed via infocmp file: /lib/termininfo/v/v/vt100
vt100|vt100-am|dec vt100 (w/advanced video)
am, msgr, xnl, x.
```

```
cols#80, it#8, lines#24, vt#3,
acsc=~^aaffggjkllmmnnooppqqrssttuvvwwxyzzz(||)~,
bel=^, blink=E[m$50>-_N, bold=E[1m$2>,
clear=[E[H]J<50>-_N, csr=E[%p1d;%%p2dr,
cub=E[%p1dd], cub1=~J, cud=E[%p1dB], cud1=J,
curf=E[%p1dc], curf1=E[1$2>,
cup=E[%p1d;%%p2dr=H<50>, cuv=E[%p1dA,
cuul=A=E[3J<50>, el=, el1=E[1K$3>,
```
