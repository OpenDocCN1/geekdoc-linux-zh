# START-UP SCRIPT BASICS

These are stored in the ~/logout script, so if you’re feeling adventurous, you can experiment with this one, too.

# Can I get rid of that boring old $ prompt?

Yes! The Korn shell defines a variable, **PS1**, which is the normal prompt. So, if you change the value of **PS1**, you change your prompt. This prompt can include the values of other variables, or any text string. For example, if you like to think of yourself as the master of the computer, you might try this for a prompt:

```
PS1='How may I serve you, Master?'
```

Go ahead; try a few things. You can have some fun with this, but when you get done fooling around, you’ll probably want something more useful, so keep reading.

Use the **$PWD** variable that is built into the Korn shell to track your current directory. Most of us are familiar with the DOS prompt that tracks our current directory. So, if you try to achieve the same thing in UNIX, you might try

```
PS1='$PWD \$ '
```

Looks good at first glance. If you are in your home directory, it might look something like this:

```
/users/harold $
```

But what happens when you change to harold’s bin directory? You type in

```
/users/harold $ cd bin
```

then ask for the identity of the present working directory,

```
/users/harold $ pwd
```

and end up with the following:

```
/users/harold/bin
/users/harold $
```

Maybe this isn’t quite what you had in mind. That’s because the double quotes allow the Korn shell to "see" the **$PWD** variable and interpret it. Once that happens, it’s converted into a string and becomes static. To prevent this,