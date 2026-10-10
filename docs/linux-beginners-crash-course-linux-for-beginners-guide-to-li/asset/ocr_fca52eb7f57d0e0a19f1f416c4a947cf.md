# Creating a blank file

A feature of many commands that are involved with the manipulation of data is that, if we refer to a directory that does not yet exist, they will create it for us. We can use this to create blank files with a command named *touch*:

```
touch [options] <filename>
```

For example:

```
pwd
```

```
/home/Simon/linuxtutorialwork
```

```
ls
```

```
foo
```

```
touch example1
```

```
ls
```

```
example1 foo
```

The *touch* command is used to modify the modification and access times on files. It isn’t always needed, but it can be helpful to use if you are testing a system that relies on file modification or file access times. What is important, as I said earlier, is that if you *touch* on a file or directory that does not exist, it will be created for you.

Much of what we do in Linux cannot be done automatically, but when you know how a certain command behaves and some of the deeper aspects of the system, you can use the command in creative ways to get the outcome you desire.