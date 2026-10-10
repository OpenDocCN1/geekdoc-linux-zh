(For this step, enter the PID you recorded in Exercise 25 or found with the `ps a` command you just executed.)

```
```
$ ps a<Enter>
```
```

+   27. Repeat Exercise 25. Kill the process using the job number rather than the process ID. Check to be sure the job was killed.

```
```
$ l& -R / > outfile 2> errfile &<Enter>
$ jobs<Enter>
$ kill $jobnumber<Enter>
$ ps a<Enter>
```
```

or

```
```
$ jobs<Enter>
```
```

See Appendix B for answers.

# ## Quiz

+   1. Which command is used to pass the value of a variable from a parent shell to a subshell?

+   2. Determine the value of `x` at the end of the following procedure:

```
```
$ (starting in the login shell)
$ x=5<Enter>
$ bash<Enter>
$ x=50<Enter>
$ export x<Enter>
$ <Ctrl>-d
```
```

+   3. True or false: each process returns an exit code to its parent process after successful completion.

+   4. Which of the following is the proper syntax for checking a shell’s process identification number?
+       * `$ echo $$<Enter>`
+       * `$ echo $?<Enter>`