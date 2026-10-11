
programming language, a shell function is called by giving its name followed by any arguments.

### Shell features
There are several ways to customize the shell's behavior. You can use options on the command line when you call bash and you can use the **bash** set and **shopt** builtins to turn features on and off.

### Command-line expansion
When it processes a command line, the Bourne Again Shell may replace some words with expanded text. Most types of command-line expansion are invoked by the appearance of a special character within a word (for example, a leading dollar sign denotes a variable). See Table 9-6 on page 313 for a list of special characters. The expansions take place in a specific order. Following the history and alias expansions, the common expansions are parameter and variable expansion, command substitution, and pathname expansion. Surrounding a word with double quotation marks suppresses all types of expansion except parameter and variable expansion. Single quotation marks suppress all types of expansion, as does quoting (escaping) a special character by preceding it with a backslash.

## EXERCISES

1.  Explain the following unexpected result:

    ```bash
    $ whereis date
    date: /bin/date ...
    $ echo $PATH
    :./usr/local/bin:/usr/bin:/bin
    date > date
    echo "This is my own version of date."
    $ date
    Sat May 24 11:45:49 PDT 2008
    ```

2.  What are two ways you can execute a shell script when you do not have execute access permission for the file containing the script? Can you execute a shell script if you do not have read access permission for the file containing the script?

3.  What is the purpose of the **PATH** variable?
    a. Set the **PATH** variable so that it causes the shell to search the following directories in order:
        - `/usr/local/bin`
        - `/usr/bin`
        - `/bin`
        - `/usr/kerberos/bin`
        - The **bin** directory in your home directory
        - The working directory

    b. If there is a file named do it in /usr/bin and another file with the same name in your ~/bin, which one will be executed? (Assume that you have execute permission for both files.)

    c. If your PATH variable is not set to search the working directory, how can you execute a program located there?

    d. Which command can you use to add the directory /usr/games to the end of the list of directories in PATH?

4.  Assume that you have made the following assignment:
    ```bash
    $ person=jenny
    ```
    Give the output of each of the following commands:
    a. `echo $person`
    b. `echo '$person'`
    c. `echo "$person"`

5.  The following shell script adds entries to a file named journal-file in your home directory. This script helps you keep track of phone conversations and meetings.

    ```bash
    $ cat journal
    # journal: add journal entries to the file
    # $HOME/journal-file

    file=$HOME/journal-file
    date >> $file
    echo -n "Enter name of person or group: "
    read name
    echo "$name" >> $file
    echo >> $file
    cat >> $file
    echo "------------------------------------------------" >> $file
    echo >> $file
    ```

    a. What do you have to do to the script to be able to execute it?

    b. Why does the script use the read builtin (page 937) the first time it accepts input from the terminal and the cat utility the second time?

6.  Assume that the /home/jenny/grants/biblios and /home/jenny/biblios directories exist. Give Jenny's working directory after she executes each sequence of commands given. Explain what happens in each case.

    a.
    ```bash
    $ pwd
    /home/jenny/grants
    $ CDPATH=$(pwd)
    $ cd
    $ cd biblios
    ```

    b.
    ```bash
    $ pwd
    /home/jenny/grants
    $ CDPATH=$(pwd)
    $ cd $HOME/biblio
    ```

7.  Name two ways you can identify the PID number of your login shell.

8.  Give the following command:
    ```bash
    $ sleep 30 | cat /etc/passwd
    ```
    Is there any output from sleep? Where does cat get its input from? What has to happen before the shell displays another prompt?

## ADVANCED EXERCISES

9.  Write a sequence of commands or a script that demonstrates that variable expansion occurs before pathname expansion.

10. Write a shell script that outputs the name of the shell that is executing it.

11. Explain the behavior of the following shell script:
    ```bash
    $ cat quote_demo
    twoliner="This is line 1.
    This is line 2."
    echo "$twoliner"
    echo $twoliner
    ```
    a. How many arguments does each echo command see in this script? Explain.

    b. Redefine the IFS shell variable so that the output of the second echo is the same as the first.

12. Add the exit status of the previous command to your prompt so that it behaves similarly to the following:
    ```bash
    $ [0] ls xxx
    ls: xxx: No such file or directory
    $ [1]
    ```

13. The dirname utility treats its argument as a pathname and writes to standard output the path prefix-that is, everything up to but not including the last component:
    ```bash
    $ dirname a/b/c/d
    a/b/c
    ```
    If you give **dirname** a simple filename (no / characters) as an argument, **dirname** writes a . to standard output:
    ```bash
    $ dirname simple
    .
    ```
    Implement **dirname** as a `bash` function. Make sure that it behaves sensibly when given such arguments as / .

14. Implement the **basename** utility, which writes the last component of its pathname argument to standard output, as a `bash` function. For example, given the pathname a/b/c/d, **basename** writes **d** to standard output:
    ```bash
    $ basename a/b/c/d
    d
    ```

15. The Linux **basename** utility has an optional second argument. If you give the command **basename path suffix**, **basename** removes the *suffix* and the prefix from *path*:
    ```bash
    $ basename src/shellfiles/prog.bash .bash
    prog

    $ basename src/shellfiles/prog.bash .c
    prog.bash
    ```
    Add this feature to the function you wrote for exercise 14.

# 10

# NETWORKING AND THE INTERNET

## IN THIS CHAPTER

- Types of Networks and How They Work . . . . . . . . . . . . . . . . . . . . 359
- Network Protocols . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 365
- Network Utilities . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 376
- ping: Tests a Network Connection . . . . . . . . . . . . . . . . . . . . 379
- traceroute: Traces a Route Over the Internet . . . . . . . . . . . . . . . . . . . . 380
- host and dig: Query Internet Nameservers . . . . . . . . . . . . . . . . . . . . 382
- Distributed Computing . . . . . . . . . . . . . . . . . . . . . . . . 383
- Usenet . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 392
- WWW: World Wide Web . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 395

The communications facilities linking computers are continually improving, allowing faster and more economical connections. The earliest computers were unconnected stand-alone systems. To transfer information from one system to another, you had to store it in some form (usually magnetic tape, paper tape, or punch cards—called IBM or Hollerith cards), carry it to a compatible system, and read it back in. A notable advance occurred when computers began to exchange data over serial lines, although the transfer rate was slow (hundreds of bits per second). People quickly invented new ways to take advantage of this computing power, such as email, news retrieval, and bulletin board services. With the speed of today's networks, a piece of email can cross the country or even travel halfway around the world in a few seconds.

Today it would be difficult to find a computer facility that does not include a LAN to link its systems. Linux systems are typically attached to an *Ethernet* (page 1081) network. Wireless networks are also prevalent. Large computer facilities usually maintain several networks, often of different types, and almost certainly have connections to larger networks (companywide or campuswide and beyond).

357
