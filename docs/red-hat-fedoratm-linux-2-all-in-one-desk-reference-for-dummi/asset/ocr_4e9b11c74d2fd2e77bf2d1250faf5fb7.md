# The case statement

The case statement marks labels in a switch statement. Here is an example (here interrupt_id is an integer variable):

```
switch (interrupt_id)
{
    case XMIT_RDY:
        transmit();
        break;

    case RCV_RDY:
        receive();
        break;
}
```

# A compound statement or block

A compound statement or block is a group of declarations followed by statements, all enclosed in a pair of braces ({...}). Typical compound statements are the body of a function and the block of code following an if statement. In the following example, everything that appears within the braces — the declarations and the statements — constitute a compound statement:

```
if (theEvent.exepose.count == 0)
{
    int i;
    /* Clear the window and draw the figures
    * in the "figures" array
    */
    XClearWindow(theDisplay, dWin);
    if (numFigures > 0)
        for (i = 0; i < numFigures; i++)
            draw_figure(theDisplay, dWin, theGC, i);
}
```

# The continue statement

The continue statement begins the next iteration of the innermost do, for, or while statement in which it appears. You can use continue when you want to skip the execution of the loop. For example, to add the numbers from 1 to 10, excluding 5, you can use a for loop that skips the body when the loop index (i) is 5:

```
for (i=0, sum=0; i <= 10, i++)
{
    if (i == 5) continue;  /* Exclude 5 */
    sum += i;
}
```