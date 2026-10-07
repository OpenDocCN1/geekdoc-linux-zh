# LAB 7.1: THE if COMMAND

+   - Line 6 is also optional, as indicated by the square brackets around it. It shows that after the then part and any elif parts, you can start a command with else, followed by any number of commands.

+   - The last line shows that there has to be a fi (that's if spelled backward) to mark the end of an if command.

There are several points to make about this syntax diagram. The first point is that the phrase any means "one or more complete command lines." You can write anything that would be a valid command line, including command sequences, pipelines, and the other types of command lines introduced in Chapter 2, "Command Syntax," including other if commands and any of the other control structure commands you will be learning.

The ability to put command sequences, command groups, and other structures inside the parts of a control structure is extremely powerful. However, this feature also lets you write complex programs. Beginning programmers tend to produce more complex programs than advanced programmers, who learn how to write efficient programs that are easy to understand. Strive to make your programs simple. If your code starts to get complex, think about how to write it more simply.

![](bbox=[0.19, 0.385, 0.275, 0.455])

The next point is that there must be an if, a then, and a fi—in that sequence.

If there is an else, it must be the last part of the if structure before the fi.

The elif keyword is a contraction for else if. I've included it in the syntax diagram for completeness, but if you need the logical feature it provides, you can often accomplish the same thing more clearly and at least as efficiently by using the case command introduced in Chapter 9, "The Case and Select Commands."

Avoid elif. It can lead to programs that are very hard to understand, debug, and modify. If you can, use case statements instead.

![](bbox=[0.19, 0.865, 0.275, 0.935])