The callback function `eventReleaseKey()` on line 151 is called whenever a key is released. The only ones that are of concern here are the ones that the switch statement on line 95 detects as being pressed. If it is one of the keys in question, its associated Boolean is set to `FALSE` to indicate that it no longer is being held down.

Figure 12-3 shows the information about the last key pressed, and something about the keys right before it. The top line shows the current character as being a lowercase c. The hexadecimal value of c is 0x63. Also, when the key was pressed, the Control key was held down. Starting from the right end of the middle line, you can see that the last keystroke was the letter c. Just before that, the left Control key was pressed. Directly preceding that, there was an exclamation point.

![](bbox=[0.11, 0.36, 0.56, 0.45])

# **Figure 12-3**: Monitoring keystrokes

# # GNOME's Command-Line Options

Every GNOME application has a set of command-line options available to it. The call to `gnome_init()` takes `argc` and `argv` as arguments and looks for certain options to be present. You can determine the options available in any application by starting it specifying `help` or `?`. You can use the following simple program to demonstrate this.

```
```c
/** showoptions.c **/
#include <gnome.h>

int main(int argc, char *argv[]) {
    gnome_init("showoptions", "1.0", argc, argv);
    exit(0);
}
```
```

This program has no options of its own, but the options for GNOME, GTK+, and X are available. To see them all, run the program like this:

```
```
showoptions --help | more
```
```