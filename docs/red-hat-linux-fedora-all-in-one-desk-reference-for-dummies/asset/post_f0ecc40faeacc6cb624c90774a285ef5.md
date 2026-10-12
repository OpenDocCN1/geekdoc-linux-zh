
- Call the `exec` function to overlay the current script with a new script or Linux command.
- Use `fork` and `exec` to provide shell-like behavior. (Monitor user input, and process each user-entered command through a child process.) In this section, I present a simple example of how to accomplish this task.

The simplest way to execute a Linux command in your script is to use the `system` function with the command in a string. After the `system` function returns, the exit code from the command is in the `$?` variable. You can easily write a simple Perl script that reads a string from the standard input and processes that string with the system function. Follow these steps:

### 1. Use a text editor to enter and save the following script in a file named rcmd.pl:
```
#!/usr/bin/perl
# Read user input and process command

$prompt = "Command (\"exit\" to quit): ";
print $prompt;

while (<STDIN>)
{
  chop;
  if ($_ eq "exit") { exit 0;}

  # Execute command by calling system
  system $_;
  unless ($? == 0) {print "Error executing: $_\n";}
  print $prompt;
}
```

### 2. Make the rcmd.pl file executable by using the following command:
```
chmod +x rcmd.pl
```

### 3. Run the script by typing ./rcmd.pl at the shell prompt.

Here's a sample output from the rcmd.pl script (the output depends on what commands you enter):
```
Command ("exit" to quit): ps
PID TTY TIME CMD
767 pts/0 00:00:00 bash
940 pts/0 00:00:00 rcmd.pl
945 pts/0 00:00:00 ps
Command ("exit" to quit): exit
```

You can also run Linux commands by using `fork` and `exec` in your Perl script. Following is an example script — psh.pl — that uses `fork` and `exec` to execute commands the user enters:

```
#!/usr/bin/perl

# This is a simple script that uses "fork" and "exec" to
# run a command entered by the user

$prompt = "Command (\"exit\" to quit): ";
print $prompt;

while (<STDIN>)
{
    chop;   # remove trailing newline
    if($_ eq "exit") { exit 0;}

    $status = fork;
    if($status)
    {
        # In parent... wait for child process to finish...
        wait;
        print $prompt;
        next;
    }
    else
    {
        exec $_;
    }
}
```

The following sample output shows how the psh.pl script executes the ps command:
```
Command ("exit" to quit): ps
PID TTY          TIME CMD
767 pts/0    00:00:00 bash
949 pts/0    00:00:00 psh.pl
950 pts/0    00:00:00 ps
Command ("exit" to quit): exit
```

Shells (such as Bash) use the fork and exec combination to run commands.

## File access

You may have noticed the <STDIN> expression in various examples in this chapter. That’s Perl’s way of reading from a file. In Perl, a file handle, also known as an identifier, gives a file a distinct identity while it’s being read. Usually, file handles are in uppercase characters. STDIN is a predefined file handle that denotes the standard input — by default, the keyboard. STDOUT and STDERR are the other two predefined file handles. STDOUT is used for printing to the terminal, and STDERR is used for printing error messages.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_827_0.png)

To read from a file, write the file handle inside angle brackets (< >). Thus, <STDIN> reads a line from the standard input.

You can open other files by using the open function. The following example shows you how to open the /etc/passwd file for reading and how to display the lines in that file:
```
open (PWDFILE, "/etc/passwd");  # PWDFILE is the file handle
while (<PWDFILE>) { print $_; }  # By default, input line is in $_
close PWDFILE;  # Close the file
```

By default, the open function opens a file for reading. You can add special characters at the beginning of the filename to indicate other types of access. A < prefix opens the file for writing, whereas a > prefix opens a file for appending. Following is a short script that reads the /etc/passwd file and creates a new file, named output, with a list of all users who lack shells (the password entries for these users have : at the end of each line):
```
#!/usr/bin/perl
# Read /etc/passwd and create list of users without any shell
open (PWDFILE, "/etc/passwd");
open (RESULT, ">output");  # open file for writing

while (<PWDFILE>)
{
    if ($_ =~ /:$/) {print RESULT $_;}
}

close PWDFILE;
close RESULT;
```

After you execute this script, you should find a file named output in the current directory. Here's what's the output file contains when I run this script on a Red Hat Linux system:
```
news:x:9:13:news:/etc/news:
```

## Filename with pipe prefix

One interesting filename prefix is the pipe character — the vertical bar (|). If you call open with a filename that begins with |, the rest of the filename is treated as a command. The Perl interpreter executes the command, and you can use print calls to send input to this command. The following Perl script sends a mail message to a list of users by using the mail command:
```
#!/usr/bin/perl
# Send mail to a list of users
foreach ("root", "naba") {
    open (MAILPIPE, "| mail -s Greetings $_");
    print MAILPIPE "Remember to send in your weekly report today!\n";
    close MAILPIPE;
}
```

If a filename ends with a pipe character (|), that filename is executed as a command; you can read that command's output with the angle brackets (<...>), as shown in the following example:
```
open (PSPIPE, "ps ax |");
while (<PSPIPE>)
{
# Process the output of the ps command
# This example simply echoes each line
print $_;
}
```

## Subroutines

Although Perl includes a large assortment of built-in functions, you can add your own code modules in the form of subroutines. In fact, Perl comes with a large set of these programs-within-programs. Here's a simple script that illustrates the syntax of subroutines in Perl:
```
#!/usr/bin/perl
sub hello
{
# Make local copies of the arguments from the @_ array
local ($first,$last) = @_;

print "Hello, $first $last\n";
}

$a = Jane;
$b = Doe;

&hello($a, $b);  # Call the subroutine
```

When you run the preceding script, it displays the following output:
```
Hello, Jane Doe
```

Note the following points about subroutines:
- The subroutine receives its arguments in the array @_ (the at symbol, followed by an underscore character).
- Variables used in subroutines are global by default. Use the local function to create a local set of variables.

Call a subroutine by placing an ampersand (&) before its name. Thus, the subroutine hello is called by typing &hello.

If you want, you can put a subroutine in its own file. The hello subroutine, for example, can reside in a file named hello.pl. When you place a subroutine in a file, remember to add a return value at the end of the file — just type 1; at the end to return 1. Thus, the hello.pl file appears as follows:
```
sub hello
{
# Make local copies of the arguments from the @_ array
local ($first,$last) = @_;

print "Hello, $first $last\n";
}
1;  # return value
```

Then, you have to write the script that uses the hello subroutine, as follows:
```
#!/usr/bin/perl
require 'hello.pl';  # include the file with the subroutine

$a = Jane;
$b = Doe;

&hello($a, $b);   # Call the subroutine
```

This script uses the require function to include the hello.pl file that contains the definition of the hello subroutine.

## Built-in functions in Perl

Perl has nearly 200 built-in functions (also referred to as Perl functions), including functions that resemble the ones in the C Run-Time Library, as well as functions that access the operating system. You really need to go through the list of functions to appreciate the breadth of capabilities available in Perl. I don't have enough space in this book to cover these functions, but you can learn about the Perl built-in functions by pointing your Web browser to the following address: http://www.perldoc.com/perl5.8.0/pod/perlf... This address connects you to the Perl 5.8.0 documentation page so that you can get an overview of the Perl built-in functions. On that page, click a function's name to view more detailed information about that function. You can also read the Perl function manual on your Red Hat Linux system by typing the following command in a terminal window:
