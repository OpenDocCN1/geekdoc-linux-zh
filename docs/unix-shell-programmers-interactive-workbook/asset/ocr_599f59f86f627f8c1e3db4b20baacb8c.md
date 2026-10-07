# Chapter 3: Compound Command Syntax 141

The first command line does not produce any output once true sets its exit code, there is no need to execute the print command; the shell already knows that the result of evaluating || will be true. if print command returns false, the expression will be true || false (result is true), but if print returns a value of true (which is what it always does), the expression will be true (result is also true). There is no need to run the print command, and the shell doesn't run it. The second command line requires both commands to be executed. When the shell finds that the first exit code is false, it has to execute the second command to see if the result of evaluating || will be true (if the exit code from print is true) or false (if the exit code from print is false.)

LAB 3.1

# 3.1.5 ANSWERS

Type the following commands to see a co-process at work:

```
rm -f out
cat >out |&
print -p hello
cat out
```

+   a) What is the purpose of the rm command?

Answer:Your interaction should look like the following:

```
$ rm -f out
$ cat >out |&
$ print -p hello
$ cat out
hello
$
```

That's not very exciting to look at, but it does demonstrate how a co-process works.

The rm command is used to make sure the file out't exist, to make sure the first cat command doesn't fail, in the case the noclobber option is set.

+   b) Which command runs as a co-process?

Answer:The first cat command, because it ends with the co-process symbol (|&).