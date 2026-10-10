But did it really work? Type bash into the terminal to open a new shell. This new shell looks exactly like the one you were just in, but it is actually a *child* of the original one (which we call the *parent*). Now, inside this new child shell, try to get echo to do its magic the way it did before. Nothing. What's going on?

```
```
$ bash
$ echo $myvar
```

```

A variable you create the way we just did is only going to be available locally—within the immediate shell session. If you start up a new shell—or close down the session using exit—the variable will not go along with you. Typing exit here will take you back to your original parent shell which, right now, is where we want to be. You can run echo $myvar once again if you like just to confirm that the variable is still valid. Now type export myvar to pass the variable to any child shells that you may subsequently open. Try it out: type bash for a new shell and then echo:

```
```
$ exit
$ export myvar
$ bash
$ echo $myvar
hello
```

```

All this may feel a bit silly when we are creating shells for no real purpose. But understanding how shell variables are propagated through your system will become very important once you start writing serious scripts.

# Deleting Environment Variables

Want to know how to clean up all those ephemeral variables you have created? One way is to simply close your parent shell—or reboot your computer. But there are simpler ways. Like, for instance, unset. Typing unset (without the $) will kill the variable. echo will now prove that.

```
```
$ unset myvar
$ echo $myvar
```

```

If there is an unset command, then you can bet there must be a set command to go with it.