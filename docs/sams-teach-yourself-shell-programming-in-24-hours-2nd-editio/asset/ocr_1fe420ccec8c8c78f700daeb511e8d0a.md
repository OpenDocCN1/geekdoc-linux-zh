**TABLE 8.2 continued**

| Variable | Description |
|---|---|
| PATH | Indicates the search path for commands. It is a colon-separated list of directories in which the shell looks for commands. A common value is PATH=/bin:/sbin:/usr/bin:/usr/sbin:/usr/local/bin:/usr/ucb |
| HOME | Indicates the home directory of the current user: the default argument for the cd built-in command. |

# Summary

This chapter covered using variables for shell script programming. You saw how scalar and array variables were defined, accessed, and unset. We also looked at a special category of variables known as environment variables. In subsequent chapters, we will look at how variables are used to achieve a greater degree of flexibility and clarity in shell scripts.

# Questions

+   1. Which of the following are valid variable names?
+      a. `_FRUIT_BASKET`
+      b. `1_APPLE_A_DAY`
+      c. `FOUR_SCORE&7YEARS_AGO`
+      d. `Variable`
+   2. Is the following sequence of array assignments valid in sh, ksh, and bash?
+      ```
+      $ adams[8]=hitchhikers_guide
+      $ adams[1]=restaurant
+      $ adams[3]=thanks_for_all_the_fish
+      $ adams[42]=life_universe_everything
+      $ adams[5]=mostly_harmless
+      ```
+   3. Given the preceding array assignments, how would you access the array item at index 8 in the array adams? How would you access every item in the array?
+   4. What is the difference between an environment variable and a local variable?