# Writing and Storing Scripts

It is best to use a simple text editor for composing your scripts. vi is the default text editor with Red Hat, but other editors, such as emacs, developed by Richard Stallman, work just as well. vim, a modified version of vi, is just as powerful but requires less of a learning curve. Elvis and pico are simple-to-use editors designed for beginning Linux users. My personal favorite is joe, a very functional editor based on the old WordStar program. Each of these editors is shipped with the latest Red Hat release. I recommend trying out a few and opting for the one that both best suits your needs and is most comfortable to use.

Give the file any name you want. It is best to name the file by the script’s function. For example, one script I wrote to back up all the files on one machine to another using the dump program is called, quite simply, dodump. Its name leaves little doubt as to what the program does. In order to identify this script as a customized program, give it a more descriptive name, perhaps with your initials. For example, I might rename this file to dump_kjc.sh to identify it as a script written by myself.

I prefer saving scripts in a central location. I usually create a `/usr/local/scripts/` directory where I place all executable files or scripts that do not come installed with the Red Hat Linux distribution. You can make symbolic links that point to real files in other locations, from the files in `/usr/local/scripts/` to shortcut files located in the default path, such as `/usr/local/bin/` or `/usr/bin/`.

After creating a script called dodump in the directory `/usr/local/scripts/`, I can make a linked file of the same name in `/usr/local/bin/`. Thus the dodump program is located in my path. Rather than simply placing them in `/usr/local/bin` to begin with I can separate those program created by other applications from my own scripts. This is mostly an organizational feature. Some users may choose otherwise and simply clump all programs in one standard location. I edit the permissions so that only I or the root user can read, write, or execute the file:

```
ln -s /usr/local/scripts/dodump /usr/local/bin/dodump
```

Thus when executing the script, the system pulls the dodump program out of my path while preserving the file in its default location.