# Part III: Making Decisions

Feel free to use either type of the if else statements. Both are acceptable, and the one you decide to use is up to your preference.

You can place a whole bunch of instructions between the expression and else reserved word and another whole bunch between the else and fi reserved words. The following example shows how the on-screen messages expand if you place more instructions between them:

```
```shell
if [ Quantity -ne 100 ]
then
	echo "The box is full."
	echo "Sorry, you need to stop."
else
	echo "The box is not full."
	echo "Keep going!"
fi
```
```

# ## The if elif Statement

Be careful! Your program blindly follows your instructions if the condition is false. Your program obeys the second bunch of instructions without asking a question. Sometimes you don’t want this blind obedience to happen. Instead, you want your program to make another decision before following the second bunch of instructions.

You can have your computer make another decision by using the if elif statement. This statement looks confusing at first but is fairly easy to understand after you get used to it. Following’s a simple if elif statement:

```
```shell
if [ Condition1 ]
then
	Instruction1
elif [ Condition2 ]
then
	Instruction2
fi
```
```

In this statement, your program obeys the first group of instructions if Condition1 is true. If Condition1 is false, however, your program determines whether Condition2 is true. If Condition2 is true, your program obeys the second group of instructions. If Condition2 is false, your program skips the second group of instructions.

Whenever you use the if statement, your program obeys at least one group of instructions. If you use the if elif statement, however, you always face a chance that your program may skip both groups of instructions. Following’s an example: