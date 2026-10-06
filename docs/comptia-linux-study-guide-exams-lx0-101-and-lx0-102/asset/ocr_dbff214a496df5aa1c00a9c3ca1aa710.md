# Writing Scripts

one of many possible actions defined by the readline library, which is one of the basic textmode input libraries used by Linux.

In most cases, there's no need to adjust the ~/.inputrc file, because the default readline mappings work well for x86 systems with standard keyboards. If you find that certain keystroke don't work the way they do in text mode, though, you may want to research this configuration filter.

> X uses its own keyboard input routines, so "/.inputrc doesn't affect programs run in X, even text-mode programs run inside xterm windows.

# Writing Scripts

You'll do much of your work on a Linux system by typing commands at a shell prompt. As you use Linux, you're likely to find some of these tasks to be repetitive. If you need to add 100 new users to the system, for instance, typing userid100 times can be tedious. Fortunately, Linux includes a way to cut through the tedium: shell scripts. These are simple programs written in an interpreted language that's embedded in the Linux shell you use to type commands.

Most Linux users use bash by default, so shell scripts are often written in the bash scripting language; tcsh and other scripting languages are similar. In fact, it's not uncommon to see shell scripts that run in any common Linux shell. You're not restricted to running shell scripts written in your default shell, however; the first line of a shell script identifies the shell that should be used to run it.

> Many Linux startup scripts, including SysV startup scripts, are in fact shell scripts. Therefore, understanding shell scripting is necessary if you want to modify a Linux startup script.

Like any programming task, shell scripting can be quite complex. Consequently, this chapter barely scratches the surface of what can be accomplished through shell scripting. Consult a book on the topic, such as Cameron Newham's Learning the Bash Shell, 3rd Edition (O'Reilly, 2005) or Richard Blum and Christine Bresnan's Linux Command Line and Shell Scripting Bible, 2nd Edition (Wiley, 2011), for more information.

To create a script, you must first know how to begin editing. Once you do, you'll find that one of the easiest tasks to do is to call external commands. More advanced tasks include using variables and using conditional expressions.