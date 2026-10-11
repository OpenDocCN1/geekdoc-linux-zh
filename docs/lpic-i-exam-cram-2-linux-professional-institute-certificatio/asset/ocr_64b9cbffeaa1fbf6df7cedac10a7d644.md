--contents option to the `cp` command. Answer C is incorrect because the `xcopy` command is offered only on DOS and Windows machines. Answer D is incorrect because the source directory doesn't include a `/*` suffix and therefore copies the source into the target as a subdirectory.

+   7. You are currently in the `/bbb` directory and want to move the contents from the `/ccc` directory to this one. What is the shortest command that will accomplish this?
+   
+   * A. `mv /ccc/*.* .`
+   * B. `mv ../ccc/*.* ..`
+   * C. `mv /ccc/* .`
+   * D. `mv /ccc/ /bbb`

Answer C is correct because this command moves the contents from the source to the target and is the shortest command. Answer A is incorrect because this command doesn't work for copying the contents—`*.*` is incorrect syntax for the command. Answer B is incorrect because the same condition exists—the string `*.*` doesn't stat any files or directories. Answer D is incorrect because it moves the `/ccc` directory to be a subdirectory of the `/bbb` subdirectory.

+   8. Which option to the `mkdir` and `rmdir` commands allows you to create a nested subdirectory tree?
+   Example: `/dir1/dir2/dir3/dir4`
+   
+   * A. `-c`
+   * B. `-n`
+   * C. `-d`
+   * D. `-p`

Answer D is correct because the `-p` option allows `mkdir` and `rmdir` to create and remove parent directories. Answers A, B, and C are incorrect: These options are not available to the `mkdir` and `rmdir` commands.

+   9. You are the sysadmin of a busy server and need to save space on your `/home` partition. You need to remove all files named `core` that are older than seven days in the users' home directories, without receiving any prompts. Write the exact command that will accomplish this in the blank below:
+   
+   `find /home -mtime +7 -name core -exec rm -f {} \;`
+   There are no alternative correct answers.