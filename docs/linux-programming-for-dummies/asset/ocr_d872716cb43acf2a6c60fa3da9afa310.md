# Part III: Making Decisions

Basically, you're telling your program to follow the **Instruction** if a certain **Condition** exists — meaning that the **Condition** is *true*.

The **Condition** must always be *true* or *false*.

Following are some real-life examples. The first one tells your program to check whether the box is full. The box can hold only 100 cookies (something dear to my stomach).

```
if [ $Quantity -eq 100 ]
then
 echo "The box is full."
fi
```

This statement tells your program to look at the variable **Quantity** and decide whether the value is 100 cookies. If that's true, your program displays the following message on-screen:

```
The box is full.
```

If the value isn't 100 cookies, however, your program skips this instruction and moves to the instruction that follows the **fi**. This **fi** is a reserved word that has a special meaning to your program (because it ends the **if** statement).

Try another example. In this case, your program must check to determine whether the box is full and check to see whether any sufficient boxes are available. Both conditions must be true for your program to report back that you can't package any more cookies.

```
if [ $Quantity -eq 100 ] && [ $AvailableBoxes -lt 1 ]
then
 echo "The box is full and you have no more boxes."
fi
```

This statement tells your program to look at the variable **Quantity** and decide whether the value is 100 cookies. Your program also looks at the variable **AvailableBoxes**, to see whether its value is less than 1. If both conditions are *true*, your program displays the message **The box is full and you have no more boxes**, on-screen.

If the value isn't 100 cookies, however, and boxes remain, your program skips this instruction and moves to the instruction that follows the **fi** reserved word.

You can place a bunch of instructions within the **if** statement; your program obeys these instructions only if the condition is true.