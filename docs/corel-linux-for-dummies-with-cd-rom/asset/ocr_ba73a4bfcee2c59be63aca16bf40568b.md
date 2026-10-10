# Appendix A

# Commands to the Rescue!

Hey, didn't you tell me that Corel Linux offers a graphical user interface? Why should I use Linux commands? You're right: Corel Linux will probably run in graphical mode all the time. But accidents can happen. What if your graphics fail and Corel Linux boots into command mode? You can

+   - Wipe out your system and start all over again.
+   - Try to rescue your files and your configuration.

If Corel Linux starts in command mode, rescuing your files is easy. And with a little outside advice, you might be able to restore your system just by editing a configuration file.

# Command Anatomy 101

After you get to know the Linux commands, you'll find that they're nothing to be afraid of. In fact, consider them your friends, waiting to do what they can for you.

Commands can have up to three components:

+   - The **command** itself, such as `ls`, `cd`, or `cp`
+   - **Variable information** that you plug into the command, such as a directory name and a path
+   - **Options** (arguments) that expand or alter what the command does for you

For example, the command

```
```
ls /home/erwin/work -l
```
```

lists the files in the /home/erwin/work directory and displays their file size and permissions.