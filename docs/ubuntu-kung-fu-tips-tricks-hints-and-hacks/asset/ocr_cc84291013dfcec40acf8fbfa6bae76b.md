As mentioned, the cd (change directory) command is used to switch into another folder. It needs to be told what folder, so we supply this as an argument. The following will switch into the Documents folder:

+   - cd Documents

Some commands need more than one argument. Say that we wanted to copy the file report.doc from the Documents folder to the Desktop folder. The cp command is used to copy files and folders. We tell it the location and name of the file to be copied as the first argument, and specify the destination as the second argument:

+   - cp ~/Documents/report.doc ~/Desktop/

In this example, we’ve used the tilde symbol again as shortcut for the /home folder. From left to right, on my test system the command would translate as copy (cp) the file report.doc found at /home/keir/Documents/ to the destination folder /home/keir/Desktop/.

Once a command is entered, all that’s usually seen is the prompt again. There’s no confirmation. bash doesn’t say “OK” or “Command completed!”. bash is the silent type. It’ll only speak if it has to, usually to tell you of an error.

# Command options

Most commands also have command options. These alter how the command works. Going back to the file listing command (ls), one problem is that it lists files without any additional information. What if we want to know who owns the files, or what permissions are set? For this we use the -l command option. Most command options are preceded by one or two hyphens, so that bash knows they’re not arguments.

Here’s the ls command used on its own, and then with the -l command option:

+   - ls

```
Desktop  Documents  Examples  Music  Pictures  Public
Templates  Videos
```

+   - ls -l

```
total 28
drwxr-xr-x 2 keir keir 4096 2008-10-24 10:07 Desktop
drwxr-xr-x 2 keir keir 4096 2008-10-24 10:07 Documents
lrwxrwxrwx 1 keir keir   26 2008-10-24 09:51 Examples -> /usr/share/example-content
etc.
```