recover even if you do crash or have a power failure), here's a simple macro to save your current work and continue without losing your place in the file.

```
:map! #= ^[:w!^Ma
```

This command, which is mapped on the F3 key, begins with an escape to take you to command mode, then the ":w!Enter" sequence to write the current file out to disk, and finally an "a" to take you back into text insertion mode right where you left off. Note that both the "ESC" key and the "ENTER" key must be escaped with CTRL-V or they will be misinterpreted.

# Can I use the map! command to make a text insertion mode command that behaves like the CTRL-G of command mode to see where I am in the current file?

This one is handy if you just want to know where you are in the file without having to go out to command mode and come back. Well, actually you do have to go out and back, but it's all automatic.

```
:map! ^G ^[^V^Ga
```

This one's a little tricky. Because CTRL-G has a special meaning, you can't just enter it, and if you enter a single CTRL-V it will escape what you are trying to do. So the trick to this one is that the first CTRL-G must be entered with a CTRL-V,CTRL-G sequence, then CTRL-V, ESCAPE,CTRL-V,CTRL-G, and a final "a" to go back into text insertion mode.

# How can I reduce the number of keystrokes I need to enter for common phrases?

Use :abbr. This one is so simple you should do it on the fly whenever you find yourself repeatedly using the same sequence. And it's handy for creating standard phrases so that an entire workgroup uses the same wording for critical phrases. For example, while writing this chapter we must have used the sequence ".pgvi.pgx" a zillion times, since we wanted it to appear in "program text," not in regular text,