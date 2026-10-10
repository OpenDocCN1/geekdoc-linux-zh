+   Call the exec function to overlay the current script with a new script or Linux command.

+   Use fork and exec to provide shell-like behavior. (Monitor user input and process each user-entered command through a child process.) In this section, I present a simple example of how to accomplish this task.

The simplest way to execute a Linux command in your script is to use the *system function with the command in a string. After the *system function returns, the exit code from the command is in the $ ? variable. You can easily write a simple Perl script that reads a string from the standard input and processes that string with the system function. Follow these steps:

1. Use a text editor to enter and save the following script in a file named rcmd.pl:

```
#!/usr/bin/perl
# Read user input and process command
$prompt = "Command (\\"exit\\" to quit) : ";
print $prompt;

while (<STDIN>)
{
    chomp;
    if ($_ eq "exit") { exit 0;}

    # Execute command by calling system
    system $_;
    unless ($? == 0) { print "Error executing: $_\n";}
    print $prompt;
}
```

2. Make the rcmd.pl file executable by using the following command:

```
chmod +x rcmd.pl
```

3. Run the script by typing ./rcmd.pl at the shell prompt.

Here's a sample output from the rcmd.pl script. (The output depends on what commands you enter)

```
Command ("exit" to quit): ps
  PID TTY          TIME CMD
 3128 pts/2    00:00:00 bash
 3314 pts/2    00:00:00 rcmd.pl
 3315 pts/2    00:00:00 ps
Command ("exit" to quit): exit
```

You can run Linux commands by using fork and exec in your Perl script. Following is an example script — psh.pl — that uses fork and exec to execute commands the user enters: