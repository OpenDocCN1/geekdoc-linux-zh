
![](img/ec25e59d75726b7041242a56d3376832_104_0.png)

Server: Apache/2.2.20 (Ubuntu)
**Location: http://admin.megacorphone.com:81/admin/**
Vary: Accept-Encoding
Content-Length: 333
Content-Type: text/html; charset=iso-8859-1

```html
<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
<title>301 Moved Permanently</title>
</head><body>
<h1>Moved Permanently</h1>
<p>The document has moved <a href="http://admin.megacorphone.com:81/admin/">here</a>.
</p>
<hr>
<address>Apache/2.2.20 (Ubuntu) Server at admin.megacorphone.com Port 81</address>
</body></html>
```

*Listing 133 - Using tcpdump with some advanced filtering*

From here, our story becomes clearer. We see a significant amount of failed attempts to authenticate to the **admin** directory, which resulted in HTTP 401 replies, while the last attempt to login seems to have succeeded, as the server replied with a HTTP 301 response. It seems someone gained access to one of megacorphone’s servers!

### 4.5.3.1 Exercises

- Use **tcpdump** to recreate the Wireshark exercise of capturing traffic on port 110.
- Use the `-X` flag to view the content of the packet. If data is truncated, investigate how the `-s` flag might help.
- Find all ‘SYN’, ‘ACK’, and ‘RST’ packets in the `password_cracking_filtered.pcap` file.
- An alternative syntax is available in tcpdump where you can use a more user-friendly filter to display only ACK and PSH packets. Explore this syntax in the tcpdump manual by searching for “tcpflags”. Come up with an equivalent display filter using this syntax to filter ACK and PSH packets.

## 4.6 Wrapping Up

In this module, we demonstrated some practical tools that are found in every pentester’s toolkit including *Netcat, Socat, PowerShell, Wireshark*, and *Tcpdump*. These tools can assist in many ways during a penetration test, especially when a target is lacking in specialized tools or when we need to transfer small tools to expand our foothold on the target network.

## 5. Bash Scripting

The GNU Bourne-Again Shell (Bash)[^110] is a powerful work environment and scripting engine. A competent security professional skillfully leverages Bash scripting to streamline and automate many Linux tasks and procedures. In this module, we will introduce Bash scripting and explore several practical scenarios.

### 5.1 Intro to Bash Scripting

A Bash script is a plain-text file that contains a series of commands that are executed as if they had been typed at a terminal prompt. Generally speaking, Bash scripts have an optional extension of `.sh` (for ease of identification), begin with `#!/bin/bash` and must have executable permissions set before they can be executed. Let’s begin with a simple "Hello World" Bash script:

```bash
kali@kali:~$ cat ./hello-world.sh
#!/bin/bash
# Hello World Bash Script
echo "Hello World!"
```

Listing 134 - Creating a simple 'Hello World' Bash script

This script has several components worth explaining:

- * Line 1: `#!` is commonly known as the *shebang*[^111], and is ignored by the Bash interpreter. The second part, `/bin/bash`, is the absolute path[^112] to the interpreter, which is used to run the script. This is what makes this a "Bash script" as opposed to another type of shell script, like a "C Shell script", for example.
- * Line 2: `#` is used to add a comment, so all text that follows it is ignored.
- * Line 3: `echo "Hello World!"` uses the echo Linux command utility to print a given string to the terminal, which in this case is "Hello World!".

Next, let’s make the script executable and run it:

```bash
kali@kali:~$ chmod +x hello-world.sh

kali@kali:~$ ./hello-world.sh
Hello World!
```

Listing 135 - Running a simple 'Hello World' Bash script

The chmod command, along with the +x option is used to make the script executable, and ./hello-world.sh is used to actually run it. The ./ notation may seem confusing but this is simply a path notation indicating that this script is in the current directory. Whenever we type a command, Bash tries to find it in a series of directories stored in a variable[^113] called PATH. Since our home directory is not included in that variable, we must use the relative path[^114] to our Bash script in order for Bash to "find it" and run it.

Now that we have created our first Bash script, let's explore Bash in a bit more detail.

### 5.2 Variables

Variables are named places to temporarily store data. We can set (or "declare") a variable, which assigns a value to it, or read a variable, which will "expand" or "resolve" it to its stored value.

We can declare variable values in a number of ways. The easiest method is to set the value directly with a simple *name=value* declaration. Notice that there are no spaces before or after the "=" sign:

```
kali@kali:~$ first_name=Good
```

Listing 136 · Declaring a simple variable

Declaring a variable is pointless unless we can reference it. To do this, we precede the variable with the "${ }" character. Whenever Bash encounters this syntax in a command, it replaces the variable name with its value ("expands" the variable) before execution:

```
kali@kali:~$ first_name=Good
kali@kali:~$ last_name=Hacker
kali@kali:~$ echo $first_name $last_name
Good Hacker
```

Listing 137 · Declaring and displaying our own variables

Variable names may be uppercase, lowercase, or a mixture of both. However, Bash is case-sensitive so we must be consistent when declaring and expanding variables. In addition, it’s good practice to use descriptive variable names, which make our scripts much easier to read and maintain.

Be advised that Bash interprets certain characters in specific ways. For example, this declaration demonstrates an improper multi-value variable declaration:

```
kali@kali:~$ greeting=Hello World
bash: World: command not found
```

Listing 138 · Attempting to assign a complex value to a variable

This was not necessarily what we expected. To fix this, we can use either single quotes (' ') or double quotes (" ") to enclose our text. However, Bash treats single and double quotes differently. When encountering single quotes, Bash interprets every enclosed character literally. When enclosed in double quotes, all characters are viewed literally except "$", " ", and "\" meaning variables will be expanded in an initial substitution pass on the enclosed text.

A simple example will help clarify this:

```
kali@kali:~$ greeting='Hello World'
```

![](img/ec25e59d75726b7041242a56d3376832_107_0.png)

```
kali@kali:~$ echo $greeting
Hello World

kali@kali:~$ greeting2="New $greeting"

kali@kali:~$ echo $greeting2
New Hello World
```

Listing 139 - Using single and double quotes to illustrate complex variable assignment using a string

In this example, the single-quote-enclosed declaration of *greeting* preserved the value of our text exactly and did not interpret the space as a command delimiter. However, in the double-quote-enclosed declaration of *greeting2*, Bash expanded *$greeting* to its value (“Hello World”), honoring the special meaning of the “$” character.

We can also set the value of the variable to the result of a command or program. This is known as *command substitution*[^115], which allows us to take the output of a command or program (what would normally be printed to the screen) and have it saved as the value of a variable.

To do this, place the variable name in parentheses “( )”, preceded by a “$” character:

```
kali@kali:~$ user=$(whoami)

kali@kali:~$ echo $user
kali
```

Listing 140 - Illustrating the use of command substitution and variables

In Listing 140, we assigned the output of the **whoami** command to the *user* variable. We then displayed its value. An alternative syntax for command substitution using the backtick, or grave, character (`) is shown below:

```
kali@kali:~$ user2=`whoami`

kali@kali:~$ echo $user2
kali
```

Listing 141 - An alternative syntax for command substitution

The backtick method is older and typically discouraged as there are differences in how the two methods of command substitution behave[^116]. It is also important to note that command substitution happens in a subshell and changes to variables in the subshell will not alter variables from the master process. This is demonstrated in the following example:

```
kali@kali:~$ cat ./subshell.sh
#!/bin/bash -x

var1=value1
echo $var1

var2=value2
echo $var2
```

[^110]: (GNU, 2017), http://www.gnu.org/software/bash/
[^111]: (Wikipedia, 2019), https://en.wikipedia.org/wiki/Shebang_(Unix)
[^112]: (The Linux Information Project, 2005), http://www.linfo.org/absolute_pathname.html
[^113]: (O'Reilly Media, Inc., 1998), https://www.oreilly.com/library/view/learning-the-bash/156923472/ch04s02.html
[^114]: (The Linux Foundation, 2016), https://www.linux.com/blog/absolute-path-vs-relative-path-linuxunix
[^115]: (GNU, 2019), https://www.gnu.org/software/bash/manual/html_node/Command-Substitution.html
[^116]: (BashFAQ, 2016), http://mywiki.wooledge.org/BashFAQ/082
