# Setting the clear screen timeout

You might have noticed that when your screen fills up, CP displays the text More... in the lower right corner of the screen and waits for you to press the key on your keyboard that clears the screen before displaying more output.

> Note: Clearing the screen on a 3270: use the Pause (Break) key; with IBM Personal Communications 3270 emulator software, right-click the mouse on the screen and select Clear.

By default, CP waits 60 seconds for you to clear the screen before clearing it automatically. To customize this behavior use the TERM MORE command and with the timeout parameters, described in Table 2-2:

```
TERM MORE t1 t2
```

Table 2-2 TERM MORE command parameters

| Parameter | Description |
|---|---|
| t1 | The number of seconds that CP waits before sounding a bell to alert you that the screen will automatically clear. The default is 50 seconds. |
| t2 | The number of seconds after the bell is sounded before the auto-clear actually takes place. The default is 10 seconds. |

To prevent CP from holding the screen and forcing you to press the clear key, set both timeouts to zero (0) seconds:

```
TERM MORE 0 0
```

Keep in mind, however, that by setting the timeouts to zero, you might not have time to read all of the messages displayed on the terminal. In some cases, this might be acceptable (for example, if you are running a command or a program that is generating a large amount of output that you do not care about).

To return to the default behavior of 60 seconds (50 seconds before the bell, 10 additional seconds before the clear), use the following command:

```
TERM MORE 50 10
```

> Note: The maximum value you can specify for both timeouts is 255 seconds. This means that the maximum wait before an auto-clear is 8 minutes and 30 seconds.