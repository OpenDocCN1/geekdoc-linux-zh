![](bbox=[0.3, 0.09, 0.75, 0.26])

The `dirs` builtin uses a tilde (~) to represent the name of a user’s home directory. The examples in the next several sections assume that you are referring to the directory structure shown in Figure 9-2.

# pushd: PUShes A DIRECTORY ON THE STACK

When you supply the `pushd` (push directory) builtin with one argument, it pushes the directory specified by the argument on the stack, changes directories to the specified directory, and displays the stack. The following example is illustrated in Figure 9-3:

```
$ pushd ../demo
~/demo ~/1/literature
$ pwd
/home/sam/demo
$ pushd ../names
~/names ~/demo ~/1/literature
$ pwd
/home/sam/names
```

When you use `pushd` without an argument, it swaps the top two directories on the stack, makes the new top directory (which was the second directory) the new working directory, and displays the stack (Figure 9-4):

```
$ pushd
~/demo ~/names ~/1/literature
$ pwd
/home/sam/demo
```

Using `pushd` in this way, you can easily move back and forth between two directories. You can also use `cd -` to change to the previous directory, whether or not you have explicitly created a directory stack. To access another directory in the stack, call `pushd` with a numeric argument preceded by a plus sign. The directories in the stack are numbered starting with the top directory, which is number 0. The following `pushd` command continues with the previous example, changing the working directory to `literature` and moving `literature` to the top of the stack:

```
$ pushd +2
~/literature ~/demo ~/names
$ pwd
/home/sam/literature
```