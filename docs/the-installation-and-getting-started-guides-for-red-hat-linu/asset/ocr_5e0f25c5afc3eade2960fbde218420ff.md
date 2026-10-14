# Looking Around With ls

Now that you know how to move around, it's time to take a look at what's in the directories. But first, let's make sure you've got something you can look for in your login directory before we go any further. You can start by creating an empty file. To do so, you can use a utility called touch at the shell prompt. Try it; type:

```
touch foo.bar
```

Now, in your login directory, you've got an empty file called foo.bar. You'll see it in a couple minutes. Let's also create a new directory, using the mkdir command. At the prompt, type:

```
mkdir tigger
```

Now, you've created a directory called tigger in your login directory. From root, your new directory's absolute pathname would be /home/yourlogin/tigger, and your directory is the parent of tigger. (You can learn more about creating — and removing — files and directories in Chapter 3.)

Now, you're ready to go.

In the DOS world, using the dir command will display the contents of a directory.

The same can be said of Linux — with some notable exceptions.

In Linux, dir won't fully display the contents of directories, and doesn't have the power or flexibility of the list command — ls.

In your login directory, for example, type:

```
dir
```

Now, in the same xterm window, type:

```
ls
```