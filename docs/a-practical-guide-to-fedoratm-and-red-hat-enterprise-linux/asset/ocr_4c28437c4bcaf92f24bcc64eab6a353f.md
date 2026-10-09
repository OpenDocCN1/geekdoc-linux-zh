![](bbox=[0.3, 0.08, 0.8, 0.62])

Figure 27-3 An if…then…elif flowchart

If the *test-command* returns a *true* status, the **if** structure executes the commands between the **then** and **else** statements and then diverts control to the statement following **fi**. If the *test-command* returns a *false* status, the **if** structure executes the commands following the **else** statement.

When you run the **out** script with arguments that are filenames, it displays the files on the terminal. If the first argument is `-v` (called an option in this case), **out** uses `less` (page 220) to display the files one screen at a time. After determining that it was called with at least one argument, **out** tests its first argument to see whether it is `-v`. If the result of the test is *true* (the first argument is `-v`), **out** uses the `shift` builtin (page 1025) to shift the arguments to get rid of the `-v` and displays the files using `less`. If the result of the test is *false* (the first argument is *not* `-v`), the script uses `cat` to display the files.