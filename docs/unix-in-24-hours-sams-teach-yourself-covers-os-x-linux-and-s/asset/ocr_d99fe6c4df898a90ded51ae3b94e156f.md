# Hour 17. Advanced Shell Programming

# Goals for This Hour

In this hour, you will learn

+   ► How to find files fast with `mylocate`
+   ► How to count commands on your system with `cmdcnt`
+   ► About finding your disk usage stats with `diskspace`
+   ► How to waste time with the `hi-low` game

In the preceding hour, you learned about the basics of dropping a set of Unix commands into a file and turning them into a shell script. It turns out that shell scripts can be remarkably capable, and in just a few lines you can often produce sophisticated mini-programs that make your time at the command line more productive and even more fun. This hour expands on the shell script topic by presenting four shell scripts that should whet your appetite for scripting and demonstrate how Unix makes it simple to expand and customize your computing experience.

There are plenty of different shell scripts that you could use to explore more sophisticated scripting techniques, but I believe that the best approach is to study a few small, well-written scripts. You can always find shell scripts on your own system by using a command sequence like this:

Click here to view code image

```
cd /usr/bin
file * | grep -i shell\ script
```

On the latest Solaris system, this produces a list of 164 different shell scripts included with the operating system. There’s lots to study when you want to learn more about shell scripting!

# Note

The shell scripts presented in this hour are inspired by scripts included with my book *Wicked Cool Shell Scripts* (No Starch Press, 2015). If you find yourself really getting into scripting, pick up that book, which is an excellent follow-on to this hour, if I say so myself!

# Searching a Database of Filenames with mylocate

Many versions of Unix and Linux include a terrific application called `locate`, which maintains a database of all file and directory names on your computer, letting you quickly and easily search for files and programs by name across all known file systems.

Locate can have a significant security flaw, however, in that it can end up running as root and index *everything on your system* rather than just the files and directories that you