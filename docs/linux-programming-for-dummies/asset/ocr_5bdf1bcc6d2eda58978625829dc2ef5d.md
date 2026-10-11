Following are some good fallback plans that you can try:

+   - **Set flags for yourself throughout the program.** A *flag* is a message that appears on-screen to tell you what part of your program your computer is currently reading (see Chapter 4).
+   - **Display the value of all the variables in your program on-screen.** This procedure gives you a glimpse of what’s happening behind the scenes (see Chapter 4).
+   - **Turn parts of your program off and on by making the expression** ***true or false.*** *This process helps you to isolate the part of your program that’s causing the trouble (see Chapter 3).*

Just use a little common sense in using any of these methods. You must decide where to place the flags and which parts of your program you turn off and on.

# Setting flags

A *flag* is simply a message that appears on-screen. The message of a flag can be as simple as “I got this far.”

The following example shows you how to use flags in your program (and notice that the `let` command designates the flag):

```
```bash
#!/bin/bash
let flag=1
echo "Outside of while loop"
while [ "$flag" -eq 1 ]
do
    echo "Inside of while loop"
    for friend in Bob Mary Sue
do
        echo "Inside of for-in loop"
        echo "Hello $friend."
    done
    echo "Outside of for-in loop"
    echo "Good-bye!"
    let flag=1
echo "last line in while loop"
done
echo "last line in the program"
```
```

You see the following messages on-screen as you run this program:

```
```
Outside of while loop
Inside of while loop
Inside of for-in loop
Hello Bob
Inside of for-in loop
```
```