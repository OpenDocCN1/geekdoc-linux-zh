# 310 CHAPTER 9 THE BOURNE AGAIN SHELL

![](bbox=[0.348, 0.097, 0.79, 0.308])

If you try to exit from a shell while jobs are stopped, the shell issues a warning and does not allow you to exit. If you use jobs to review the list of jobs or you immediately try to exit from the shell again, the shell allows you to exit. If hunaponexit (page 355) is not set (the default), stopped and background jobs keep running in the background. If it is set, the shell terminates the jobs.

# MANIPULATING THE DIRECTORY STACK

The Bourne Again Shell allows you to store a list of directories you are working with, enabling you to move easily among them. This list is referred to as a stack. It is analogous to a stack of dinner plates: you typically add plates and remove plates from the top of the stack, so this type of stack is named a last in, first out (LIFO) stack.

# dirs: DISPLAYS THE STACK

The dirs builtin displays the contents of the directory stack. If you call dirs when the directory stack is empty, it displays the name of the working directory:

```
$ dirs
~/literature
```

![](bbox=[0.406, 0.693, 0.726, 0.889])