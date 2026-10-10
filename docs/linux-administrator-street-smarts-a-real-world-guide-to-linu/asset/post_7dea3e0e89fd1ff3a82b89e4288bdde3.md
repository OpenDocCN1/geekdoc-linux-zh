
## TABLE 1.5 Common Environment Variables and Their Meanings (continued)

| Variable Name | Explanation |
| --- | --- |
| SLD_LIBRARY_PATH | A few programs use this environment variable to indicate directories in which library files may be found. It works much like PATH. |
| PS1 | This is the default prompt in bash. It generally includes variables of its own, such as \u (for the username), \h (for the hostname), and \W (for the current working directory). This value is frequently set in /etc/profile, but it is often overridden by users. |
| TERM | This variable is the name of the current terminal type. To move a text-mode cursor and display text effects for programs like text-mode editors, Linux has to know what commands the terminal supports. The TERM environment variable specifies the terminal in use. This information is combined with data from additional files to provide terminal-specific code information. $TERM is normally set automatically at login, but in some cases you may need to change it. |
| DISPLAY | This variable identifies the display used by X. It’s usually :0.0, which means the first (numbered from 0) display on the current computer. When you use X in a networked environment, though, this value may be preceded by the name of the computer at which you’re sitting, as in machine4.example.com:0.0. This value is set automatically when you log in, but you may change it if necessary. You can run multiple X sessions on one computer, in which case each one gets a different DISPLAY number—for instance, :0.0 for the first session and :1.0 for the second. |
| EDITOR | Some programs launch the program pointed to by this environment variable when they need to call a text editor for you to use. Thus, changing this variable to your favorite editor can help you work in Linux. It’s best to set this variable to a text-mode editor, though; GUI editors might cause problems if they’re called from a program that was launched from a text-mode login. |

![](img/f430a19bdf014c43ad7c2d594afd5b21_69_0.png)

The PATH variable often includes the current directory indicator (.) so that programs in the current directory can be run. This practice poses a security risk, though, because a malicious user could create a program with the name of some other program (such as ls) and trick another user into running it by simply leaving it in a directory the victim frequents. Even the root user may be victimized in this way. For this reason, it’s best to omit the current directory from the PATH variable, especially for the superuser. If it’s really needed for ordinary users, put it at the end of the path.

To learn what environment variables are set in your particular session, type `env`. This command officially runs a program in a modified environment; however, when typed alone, it displays the values of all the currently set environment variables. The output of this command is likely to be quite long, so you may want to pipe it through `less` or redirect the output to a file for later examination. Some of the environment variables will have fairly suggestive names, but others are likely to be obscure. You can find the purpose of some in the man page for `bash`, but others have meaning only to particular programs. If you don't understand the purpose of an environment variable, don't try to change it; ignore it or, if you're curious, try looking it up using a Web search engine.

## Criteria for Completion

To complete this task, you should have successfully tested modifications to at least two environment variables: `$PS1` (to set the shell prompt) and `$EDITOR` (to set the default editor). You should have made both transient changes (by setting the variable and using the `export` command on a command line) and more permanent changes (by editing a `bash` configuration file).

## Task 1.9: Write Basic Scripts

The `bash` and other Linux command-prompt shells are more than simple command-line tools; they're powerful programming languages. You can string together commands to have them execute one after another, add variables to improve flexibility, and use program control statements to have parts of the program execute repeatedly or only upon certain conditions.

Programs written in the `bash` shell language are often referred to as `scripts`. Compared to programs written in languages such as `C`, `C++`, and `Pascal`, `bash` scripts are easy to create but slow to execute. This makes them good choices for simple programs and for "throwaway" programs that aren't likely to be used very often. In fact, many of Linux's key startup and system configuration files are actually shell scripts. Thus, understanding how to create and modify scripts will help you administer a Linux system.

### Scenario

You find that you want to simplify or otherwise improve various tasks that you routinely perform, so you want to create scripts to handle these tasks. Specifically, you want a script to launch a few X programs with one command, a way to simplify account creation tasks, a script that reports nothing but the computer's IP address, a script that plays all the `.wav` audio files in a directory, and a script that copies files only if the destination file doesn't already exist.

### Scope of Task

Script-writing is a very open-ended activity; scripts can perform a wide variety of tasks, and there may be multiple ways of achieving the same goals within a script. This particular task presents a few scripts that illustrate important scripting features.

### Duration

This task will take about an hour to complete. Writing real-world scripts can take anywhere from a minute or so up to several hours or even days, depending on the complexity of the script and your own proficiency at script writing.

### Setup

To perform this task, you must log into your computer as an ordinary user. One of the scripts presented in this task requires *root* access to run. You’ll also need *root* access if you want to copy any of these scripts to a system directory, but this isn’t necessary to complete the task. You may use a text-mode or GUI login, although the first script launches X programs, so you’ll need an X session to test it. The scripts themselves are executed from the command line, but you’ll edit them in an editor, which may be a purely text-based editor (such as *Vi* or *nano*) or a GUI editor (such as KEdit).

### Caveats

As programs, scripts can contain bugs. Although the scripts presented in this task are fairly simple and are likely to be harmless even with typos, bugs in scripts can cause infinite loops (in which the script never terminates), excessive CPU use, accidental file deletions, and other problems. These problems can be more serious if a buggy script is run as *root*, or even if a bug-free script is used inappropriately by *root*. Thus, unless a script absolutely requires *root* access, you should always develop and test scripts as a non-root user.

### Procedure

The first thing to understand about scripts is how to create them: You use a text editor to type commands, then modify the file permissions on the resulting file so that it’s executable. Once you know how to perform these basic operations, you can proceed to create scripts that meet the objectives of this task.

## Beginning a Shell Script

Shell scripts are plain-text files, so you create them in text editors. A shell script begins with a line that identifies the shell that’s used to run it, such as the following:

```
#!/bin/sh
```

The first two characters are a special code that tells the Linux kernel that this is a script and to use the rest of the line as a pathname to the program that’s to interpret the script. Shell scripting languages use a hash mark (#) as a comment character, so the script utility itself ignores this line, although the kernel doesn’t. On most systems, */bin/sh* is a symbolic link that points to */bin/bash*, but it could point to some other shell. Specifying the script as using */bin/sh* guarantees that any Linux system will have a shell program to run the script, but if the script uses any features specific to a particular shell, you should specify that shell instead—for instance, use */bin/bash* or */bin/tcsh* instead of */bin/sh*.
