# Tip: Include the hostname in your prompt, so you know where you are. If you work in a distributed environment, where you regularly log in to different machines from your "normal" machine, it can be a pain to keep track of which machine you're on. So include it in your prompt!

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

# Which quote is which and why should I care?

Throughout this book, and in other UNIX books, you will see three different kinds of quote marks: single quotes ('), double quotes (") , and grave quotes (`). Each one has a very different meaning to the shell.

The single quote says to the shell—look, everything inside here is a plain, unadulterated string. Don't even try to check to see if you can interpret any of it. Just leave it alone and pass it on to the next process. Which means this is almost always the kind of quote you should use for an alias, because you want the first pass to simply ignore the inside of the quotes, and let it pass the contents to the second pass, which will then have the quotes stripped off, and will be able to actually interpret what you are trying to do. But if you do have variables inside the single quotes, they won't be expanded but simply passed on, complete with their dollar signs.

Double quotes, on the other hand, are still enclosing strings, but now the shell is allowed to look inside to see if there are any special characters it should interpret. This