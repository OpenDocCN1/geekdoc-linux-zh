To properly shut down your system immediately, use the **-h** option, followed by the word *now* or the numeral **0**:

```
# shutdown -h now
```

or

```
# shutdown -h 0
```

If you want to wait for a while, use the **-t** option, followed by a number (in seconds) before shutdown or reboot. If you want to restart your computer, use the **-r** option, along with the word *now* or the numeral **0**:

```
# shutdown -r now
```

or

```
# shutdown    -r 0
```

# Note

You'll find two curious text strings embedded in the shutdown program:

+   *You don't exist. Go away."
+   *"Oh hello Mr. Tyler - going DOWN?"

Both are found by executing this:

```
# strings /sbin/shutdown
```

To find out about *"You don't exist. Go away"*, see Robert Kiesling's *Linux Frequently Asked Questions with Answers*. You should be able to find a copy at http://www.linuxdoc.org/FAQ.

You can also use **linuxconf** to shut down your computer. If you're logged in as the *root* operator, enter the following from the command line of your console or an X11 terminal window:

```
# linuxconf --shutdown
```

**linuxconf** presents a shutdown dialog box, as shown in Figure 9.4. To restart your system, press the Tab key until you highlight the *Accept* button, and then press the *Enter* key. You can also enter a time delay or halt your system immediately, and specify a message to broadcast to all your users when you execute the shutdown.