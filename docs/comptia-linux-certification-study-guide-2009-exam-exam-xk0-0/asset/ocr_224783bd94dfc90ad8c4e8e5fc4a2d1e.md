the screen. Note that it will only confirm that the process is running, not if it is synchronized. **D** is correct because the `ntp` init script supports the `status` flag, which will confirm it is running and show the synchronization status. Note that not all init scripts support a `status` option; Answer **A** will work with any service.

Incorrect answers and explanations: **B** and **C**. **B** is incorrect because `ps -C ntpd` will look for an exact match for “`ntpd`.” The actual service is `ntpd`, so no match will be found. **C** is incorrect because `ps` will interpret the `ntp` as an option, which is invalid.

+   13. You have a script name some_program that needs to start in 30 min, and you decide to try the `at` command instead of setting the alarm on your watch to remind yourself. What is the correct syntax?

+   * **A.** `at 30 <return> some_program <return> <ctrl> d`
+   * **B.** `at now + 30 minutes <return> some_program <return> <ctrl> d`
+   * **C.** `at 30 minutes some_program <ctrl> d`
+   * **D.** `at now + .5 hours <return> some_program <return> <ctrl> d`

Correct answer and explanation: **B**. **B** is the correct answer because the keyword `now` understands adding time using the `+` sign and descriptive time units. The `return` is necessary to start the input for what command(s) to run, and the `<ctrl> d` is needed on a separate line to end the input.

Incorrect answers and explanations: **A**, **C**, and **D**. **A** is incorrect because the time parameter is wrong and no units are given. **C** is incorrect because the time format is wrong and the script that is to run is not on a separate line. **D** is incorrect because the time parameter must be given in whole numbers.

+   14. You are copying a bunch of files from `/temp` to `/new_stuff`, but accidentally type `cp temp/* new-stuff` instead of `new_stuff`. You’ve been reading up on the command history function and want to use that to reenter the command correctly. What do you type?

+   * **A.** `! -change new-stuff new_stuff`
+   * **B.** `!!s/new-stuff/new_stuff`
+   * **C.** `^ -`
+   * **D.** `history -r new-stuff new_stuff`

Correct answer and explanation: **C**. **C** is correct because the first `^` identifies text to be searched for and the second `^` identifies the text that will be inserted in place of the found text.