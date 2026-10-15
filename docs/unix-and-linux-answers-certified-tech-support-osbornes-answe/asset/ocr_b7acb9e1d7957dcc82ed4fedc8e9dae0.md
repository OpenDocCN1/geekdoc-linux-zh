hidden, but an ordinary **ls** command will not show them. You can "hide" directories the same way. In fact, many programs will create a raft of hidden files and directories in the hope that you'll leave these files alone.

If you'd like to experiment with un-hiding hidden files and directories, try the following, which works equally well with either the C shell or Korn shell.

```
alias la="ls -aF"
```

Then use **la** instead of **ls**, and you will see all the files, including the hidden ones. The difference is shown here:

```
 % ls
Charles
Main.c
Person.dat
trash.dt
% alias la="ls -aF"
% la
./
../
.lastlogin
.noderc
.profile
.rcoadmin.pref
.sh
.sh_history
.xdt_dir/
Charles/
Main.c
Person.dat
.rcoadmin
trash.dt
%
```

As you can see, there's a lot more useful information shown by the command we just created than by the ordinary **ls** command. If your system supports it (and most do), you can change the -aF to a -AF and get rid of the dot and dot-dot ("." and "..") from the listing.

# What if I'd like to know a file's type in addition to its name?

That's actually a little trick I snuck in above just to see if you're paying attention. The -F option to the **ls** command tells UNIX that you want to know the file type as well as the filename. If the file is executable, it gets a * after the name; if it's a symbolic link to another file, it gets a @ after the filename; and if it's a directory, it gets the slash after it.