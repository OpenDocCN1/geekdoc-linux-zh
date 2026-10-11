If you're working directly in a command line environment you still have some options. Many Linux distributions include either the pico or nano editors to provide a graphical editor environment by using ASCII control characters to create a full-screen editing window.

If your Linux distribution doesn't include either the pico or nano editor there is still one last resort: the vi editor. The vi editor is a text-based editor that uses simple single-letter commands. It's the oldest text editor in the Linux environment, dating back to the early days of Unix, which may be one reason why it's not overly elegant or user-friendly.

Once you've chosen your text editor you're ready to create your shell scripts. First, for your shell script to work you need to follow a specific format for the shell script file. The first line in the file must specify the Linux shell required to run the script. This is written in somewhat of an odd format:

```
#!/bin/bash
```

The Linux world calls the combination of the pound sign and the exclamation symbol (!) the shebang. It signals to the operating system which shell to use to run the shell script. Most Linux distributions support multiple Linux shells, but the most common is the bash shell. You can run shell scripts written for other shells, as long as that shell is installed on the Linux distribution.

After you specify the shell you're ready to start listing the commands in your script. You don't need to enter all the commands on a single line; Linux allows you to place them on separate lines. Also, the Linux shell assumes each line is a new command in the shell script, so you don't need to use semicolons to separate the commands. Here's an example of a simple shell script file.

```
```
$ cat test1.sh
#!/bin/bash
# This script displays the date and who's logged in
date
who
$
```
```

The test1.sh script file starts with the shebang line identifying the bash shell, the standard shell in Linux. The second line in the code demonstrates another feature in shell scripts. Lines that start with a pound sign are called comment lines. They allow you to embed comments into the shell script program to help you remember what the code is doing. The shell skips comment lines when processing the shell script. You can place comment lines anywhere in your shell script file, after the opening shebang line.