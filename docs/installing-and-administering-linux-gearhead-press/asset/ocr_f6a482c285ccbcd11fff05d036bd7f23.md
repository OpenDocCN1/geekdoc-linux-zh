Execute and answer the following:

+   * Did your message appear?
+   * Is your prompt identical to the name of your home directory?
+   * Change to the `/etc` directory. Did your prompt change?
+   * Use `dir`. Did you get a long listing of your current directory?

If you answered no to any of these questions, edit your `.bash_profile` and correct it.

+   17. After your customized `.bash_profile` is set up and functioning properly, open a subshell.

```
`/home/teamxx -> bash<Enter>`
```

Is your prompt identical to the name of your current directory?

Does the `dir` alias still work the way you set it?

+   18. Exit from the subshell and return to your home directory.

```
`$ <Ctrl>-d`
`/home/teamxx => cd<Enter>`
```

+   19. Most settings, with the exception of system variables, apply only to the current environment they are set in and are not passed to subshells (which are child processes). To pass customized settings down to subshells, you must set the `BASH_ENV` variable appropriately in your `.bash_profile`, and you must have a properly customized `.bashrc` file.

Revise your `.bash_profile` and create the appropriate `.bashrc` file to support the customization you implemented in Exercise 15. Remove *only* what you previously added to the `.bash_profile` in Exercise 15 except for the `echo` statement and the `PS1` variable assignment.

Add the `BASH_ENV` variable assignment. Export both the `PS1` and `BASH_ENV` variables and their values.