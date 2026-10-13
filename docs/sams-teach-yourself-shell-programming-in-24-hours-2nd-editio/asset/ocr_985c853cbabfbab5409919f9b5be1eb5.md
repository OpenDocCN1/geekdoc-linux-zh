# Changing the Prompt

You can change the prompt displayed by the select loop by altering the variable PS3. If PS3 is not set, the default prompt, #?, is displayed. For example, the commands

```
$ PS3="Please make a selection -> "; export PS3
```

change the menu displayed in the previous example to the following:

```
1) comp1
2) comp2
3) comp3
4) all
5) none
Please make a selection ->
```

Notice that the value of PS3 used has a space as its last character. This ensures that user input does not run into the prompt and thus makes the menu user friendly.

![](bbox=[0.28, 0.15, 0.35, 0.25])

> If you are using zsh, the output from the previous example will be slightly different than shown above. In zsh the menu items are listed on a single line rather than being listed on separate lines:
> 1) comp1 2) comp2 3) comp3 4) all 5) none
> #
> As you can see, the prompt is still listed on a separate line.

![](bbox=[0.28, 0.8, 0.35, 0.9])

> Versions of bash prior to 2.0 do not always use the value stored in PS3 for the prompt of the select loop. This problem is not present in ksh or zsh.

# Loop Control

So far you have looked at creating loops and working with loops to accomplish different tasks. Sometimes you will need to stop a loop or skip iterations of the loop. In this section you'll examine the break and continue commands that are used to control the execution of loops.

# Infinite Loops and the break Command

Recall that the while loop terminated when a particular condition was met. This happened when the task of the while loop completed. If you make a mistake in specifying