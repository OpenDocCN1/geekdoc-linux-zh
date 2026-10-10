The basic syntax for use of a function is

```
```
functionname() {
commands
}
...
functionname
```
```

This syntax means that a function definition begins with a name for the function, followed immediately by an open and close parentheses, a space, and an open curly brace ({}). The function body consists of one or more commands that follow the opening line, and the function ends with a close curly brace ({}). There are likely to be intervening lines of code in the program before the function is called. You call the function just like an external program, by name.

Listing 31-14 illustrates the use of functions. This script is a modification of Listing 31-11, which placed a *case* statement within a *for* loop. Although Listing 31-11 isn’t very deeply nested, a similar approach with a more deeply-nested series of commands could reduce nesting and therefore improve readability. One point to note about Listing 31-14 is that the function has access to the `$iface` variable defined in the main body of the script. This feature is actually necessary for Listing 31-14 to work.

# **Listing 31-14**
A Script Demonstrating the Use of Functions

```
```bash
#!/bin/sh

identify() {
case $iface in
lo0) echo "This computer has a loopback interface.";;
fxp0) echo "This computer has an Intel board.";;
d0) echo "This computer has a DEC/Intel Tulip chipset.";;
vrl0) echo "This computer has a VIA Rhine chipset.";;
ppp0) echo "This computer has a PPP interface.";;
*) echo "I can’t identify an interface: $iface";;
esac
}
```
```