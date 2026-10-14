NOTES: This keystroke works in the Bash shell, which is the subject of the next chapter.

# 2.3.5 Resetting the Terminal Screen

To reset the terminal screen to its default settings, use reset. This is good for when the contents of a binary file are accidentally displayed to the screen, after which only garbage characters are printed when you type. Other times, the terminal will simply stop clearing characters properly. This will fix it.

When this happens, type reset and then hit RET, even though you will not be able to read what you're typing on the screen. This works both in the console, and in terminals running in X.

+   ⇒ To reset your terminal, type:
+       $ reset RET

NOTES: You can practice this so you know what it looks like when it really happens. Do this by sending the output of a binary file to the terminal screen—type cat /bin/ls and see what it does to the terminal; then type reset to reset it.

# 2.4 Running a Command

A tool is a software program that performs a certain function—usually a specialized, simple task. For example, the hostname tool outputs the system's hostname, and the who tool outputs a listing of the users who are currently logged in. An application is a larger, usually interactive, program for completing a broader kind of task—think of image editors and word processors.

A tool or application may take any number of options (sometimes called “flags”), which specify a change in its default behavior. It may also take arguments, which specify a file or some other text to operate on. Arguments are usually specified after any options.

The term command refers to the name of a tool or application, along with any specified options and arguments. Since typing the name of a tool itself is often sufficient to accomplish a desired task, tools alone are often called commands.

Commands are case-sensitive; the names of tools and applications are usually in all lowercase letters.

To run (or “execute”) a tool or application without giving any options or arguments, type its name at a shell prompt, followed by RET.