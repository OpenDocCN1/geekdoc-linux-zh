
## START-UP SCRIPT BASICS

These are stored in the ~/logout script, so if you’re feeling adventurous, you can experiment with this one, too.

### Can I get rid of that boring old $ prompt?

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

/users/harold $

But what happens when you change to harold’s bin directory? You type in

/users/harold $ cd bin

then ask for the identity of the present working directory,

/users/harold $ pwd

and end up with the following:

/users/harold/bin
/users/harold $

Maybe this isn’t quite what you had in mind. That’s because the double quotes allow the Korn shell to "see" the **$PWD** variable and interpret it. Once that happens, it’s converted into a string and becomes static. To prevent this,

we enclose it in single quotes, which will stop the initial evaluation of the $PWD variable, and allow it to be passed to the command line, where it will then get interpreted. So now we type

```
$ PS1='\$PWD \$ '
```

and when you change to harold's bin directory and ask for the present working directory, the prompt will show

/users/harold/bin $

Now the prompt will track the current directory as intended. The deep directory structures possible in UNIX can make for a pretty long prompt, however. For this reason, we like to use the following, a two-line prompt with the current directory on the first line, and then the "$" on the second line. Type in the following:

/users/harold $ PS1='\$PWD \n\$ '

to get a prompt that looks like this:

/users/harold
$

Now we have a nice two-line prompt that shows us the current directory.

Tip: Include your "pseudo terminal" in your prompt. If you work on a machine that supports multiple pseudo terminals, keep track of which window you're working in by using this prompt:

```
PS1="[\$ (tty|cut -c9-11)]\$PWD \n\$ "
```

The result will show

[p01]

followed by your directory name information.

### Tip: Include the hostname in your prompt, so you know where you are. If you work in a distributed environment, where you regularly log in to different machines from your "normal" machine, it can be a pain to keep track of which machine you're on. So include it in your prompt!

```
PS1="${hostname} : ${PWD} \J \$ "
```

But when I do that on my system, I get

```
rc1.rc1.com:/users/charlie
$
```

So, use the %% trick to strip off the unwanted stuff from the right side of the hostname. If you're stripping something off the left side, you'd use ## instead.

```
host=`hostname`
PS1="${host%%.*}: ${PWD} \J \$ "
```

This puts the local hostname into the prompt, stripping out the domain name stuff that may be returned by running the hostname program.

### Which quote is which and why should I care?

Throughout this book, and in other UNIX books, you will see three different kinds of quote marks: single quotes ('), double quotes (") , and grave quotes (`). Each one has a very different meaning to the shell.

The single quote says to the shell—look, everything inside here is a plain, unadulterated string. Don't even try to check to see if you can interpret any of it. Just leave it alone and pass it on to the next process. Which means this is almost always the kind of quote you should use for an alias, because you want the first pass to simply ignore the inside of the quotes, and let it pass the contents to the second pass, which will then have the quotes stripped off, and will be able to actually interpret what you are trying to do. But if you do have variables inside the single quotes, they won't be expanded but simply passed on, complete with their dollar signs.

Double quotes, on the other hand, are still enclosing strings, but now the shell is allowed to look inside to see if there are any special characters it should interpret. This
