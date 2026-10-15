# Case 3. MIN == 0, TIME > 0

Unlike Case 1, TIME specifies a timer that is started when read() is called. It is not an inter-byte timer. In this case, read() returns when a single byte is received or when the timer expires. If the timer expires, read() returns 0, otherwise it returns the number of bytes read. If there are characters in the terminal's input queue before the read() call is processed, the minimum of the number of characters in the queue and numbytes_to_read bytes will be delivered to read() immediately, satisfying the call, and read() will return the number of bytes actually read.

# Case 4. MIN == 0, TIME == 0

The minimum of either the number of bytes requested, i.e. numbytes_to_read, or the number of bytes currently available is returned to the caller without waiting for more bytes to be input. If no characters are available, read() returns 0, having read no data. Otherwise the number of bytes actually read is returned. In both cases, read() returns immediately.

To demonstrate, first, in non-canonical mode we will set min = 0 and time = 30. What you will see is that if a character is typed within 3 seconds ( 30 tenths of a second), it will be delivered immediately, but if no character is typed within 3 seconds, the read will return with an EOF character. Type some characters with 3 seconds each and then let 3 seconds elapse. You will see the program terminate.

```
$ stty -icanon min 0 time 30 ; transpose
```

You may also discover that your shell terminates. Before you do this, make sure that you set the IGNOREEOF environment variable so that you do not lose your shell. If you see repeated messages of the form "Use exit to logout" then turn off the terminal settings with reset.

Next, test the effect of setting min and time to be non-zero. Type the following command sequence:

```
$ stty -icanon min 4 time 30 ; transpose
```

Wait at least 3 seconds and notice that nothing happens. The program is waiting for input. There is no timeout and the read has not returned. Now type a single character and wait several seconds. You will see its transpose after 3 seconds, demonstrating that the read returned with only 1 character after a delay of 30 time units. Now type 4 characters and see how quickly the program prints their transposes. The driver is waiting 3 seconds for the minimum number of characters to be entered; if they are entered before 3 seconds, it returns, otherwise it returns after 3 seconds with as many characters as were entered. Kill the process with Ctrl-C and turn canonical mode back on.

These experiments demonstrate that with canonical mode off, you can control input precisely. So far we have been using the stty command to control the terminal driver. In a program you can use tcgetattr() and tcsetattr() instead. The following listing is of a program that allows you to test the effects of various combinations of terminal settings, giving specific values to the MIN and TIME parameters in non-canonical mode.