
7) What will the following sequence of commands print?
set All good boys deserve fudge.
shift $$
print $#

- a) Nothing
- b) 0
- c) 5
- d) 6
- e) A "bad number" error message.

Quiz answers appear in Appendix A, Section 5.1.

## LAB 5.2 PROCESSING OPTION PARAMETERS

## LAB OBJECTIVES

- After this lab, you will be able to:
* Use the getopts Command
* Use the OPTIND Variable
* Use the OPTARG Variable
* Customize getopts Error Messages

The shell provides a number of variables that you can use along with the built-in getopts command to find out what option parameters and arguments were passed to a script or function. Option processing is usually done using one of the control structures covered in Chapter 8, “Loops,” so this lab's goal is to introduce you just to the getopts command and associated variables. You will learn the standard ways to do option processing after you have learned about the shell's control structures.

## BACKGROUND FOR THIS LAB

The shell does not differentiate between option parameters and positional parameters in a command line. It simply passes everything between the command name and the end of the command (except I/O redirection) to the command, and it is up to the command to decide what to do with each of the parameters. Because the first parameters passed to most commands are options, programmers have to write virtually the same code or script that they work on. This is not only wasted duplication of effort, it leads to different commands having different rules for the proper syntax of the options: Can you put several option letters after one dash, or do you have to use a separate dash for each one? Does there to be a space between an option letter and an argument that follows it? When the POSIX standard for shell programs and utilities was developed, it included a specification for the proper syntax for option parameters. To encourage programmers to adopt the standard, the *getopts* command was developed for use in shell scripts, and a corresponding function named getopt() was developed for C/C++ programmers. The getopts command doesn't do all the work of processing options, but it makes it easy to process them in the standard way.

> Just to make things interesting, many UNIX systems provide a getopt command (no 's' at the end) that does something similar to the getopts command. The *getopt* command is obsolete, but the getopt() function for C/C++ is not!

Most UNIX systems have an external command named getopts, probably in the /bin directory. For efficiency, the KornShell also provides a built-in version that works the same way as the external one.

## LAB 5.2 EXERCISES

### 5.2.1 USE THE getopts Command

The getopts command takes (at least) two parameters, a list of option letters, and the name of a variable. When it runs, it puts the next option that it finds in the parameter variables into the variable named in the command.

### FOR EXAMPLE

The following interaction illustrates using getopts from the command line:

```
[5051]: set --vu -do hello
[5052]: getopts douv optletter
[5053]: print $optletter
v
[5054]: getopts douv optletter
[5055]: print $optletter
u
[5056]: getopts douv optletter
[5057]: print $optletter
d
[5058]: getopts douv optletter
[5059]: print $optletter
o
```

You usually use getopts inside a script or function, but we will use the example as a model for experimenting with the getopts command by running it interactively.

- a) What is the purpose of the double dash ( -- ) on line 5051?

- b) What would be output if you printed a reference to the special variables # and @ between lines 5051 and 5052?

- c) Write a set command that would be equivalent to line 5051 but would use just two parameters instead of three.

- d) Write another set command that would be equivalent to line 5051 but would use five parameters.

- e) What would happen to optpletter if the getopts command were run again?

### 5.2.2 USE THE OPTIND VARIABLE

The getopts command keeps track of which option parameter it is processing by means of a variable named OPTIND ("option index"). Each time getopts finishes with the option letters in a parameter, it adds one to the value of OPTIND, which means that when you finish processing a command or function's options, OPTIND will be the index of the first positional parameter on the command line.

a) What are the values of OPTIND and @ after completing the previous exercise?

You can assign a value to OPTIND, and the next time you run getopts, it will start looking for option letters in the parameter number that you assigned to OPTIND. Almost always, you assign the value I to OPTIND because you want to process the options over again again from the beginning. But you can use any number you want, depending on the nature of the program you are writing.

- b) Set *OPTIND* to *1* and show that this lets you process the options over again from the beginning.

A script or function normally goes through two phases. In the first phase it uses getopts to process the option parameters. In the second phase, it processes the positional parameters. Because the second phase doesn't know how many parameters there were, it is convenient to do a shift that puts the first positional parameter into parameter variable number *1*.

#### **FOR EXAMPLE**

After processing the option parameters in the example, we would like to shift *hello*, which is in parameter *3*, into positional parameter *1*.

Hint:You can do arithmetic in the parameter you pass to *shift*.

- c) Write a *shift* command that uses OPTIND to put *hello* in parameter *1*, and verify that it works.

### 5.2.3 USE THE OPTARG VARIABLE

If an option requires an argument, put a colon ( : ) after its letter in the list you give to getopts, and getopts will automatically put the corresponding argument in the variable OPTARG. This variable is defined only after you run getopts and the option letter is one that had an argument.

Run the following commands:

```
set -c -b b_arg -a hello
OPTIND=1
```

## 242 Lab 5.2: Processing Option Parameters

a) What is the reason for assigning the value 1 to OPTIND?

Now run the following pair of commands three times

```
getopts ab:c optletter
print $OPTIND:$optletter $OPTARG
```

b) What is printed each time?

### 5.2.4 CUSTOMIZE getopts Error MESSAGES

A particularly valuable feature of getopts is that it automatically generates meaningful error messages if the user types in an invalid command line.

> FOR EXAMPLE

If the user types an option letter that is not among those specified in the getopts command, it automatically prints an error message telling what option letter was unrecognized: 

```
$ set -- -p
$ OPTIND=1
$ getopts abcghijklmnopqrstuvwxyz optletter
sh: -p: unknown option
```

This getopts command accepts any lowercase option letter except p, which just happens to be the one specified in the set command. The error message tells the user exactly what option caused the problem.

```
set -- -a -b
OPTIND=1
getopts ab: optletter
```

- a) What error message is displayed?

Write a script named s524 that contains just the command getopts ab:optletter, and run it with command line -a -b.

- b) What is the difference between the error message that prints now, compared with the previous one?

You can customize the error message by providing a string that describes argument values for the user. For example, if the user is supposed to provide a "bucket name" as the argument you could code the getopts command as:

```
getopts ab: [bucket_name] optletter
```

Replace the getopts command in your s524 script with the one above, and run it again without giving an argument after the -b.

- c) What error message did you get now?

## LAB 5.2 ANSWERS

This section gives you some suggested answers to the questions in Lab 5.2, with discussion related to those answers. Your answers may vary, but the most important thing is whether your answer works. Use this discussion to analyze differences between your answers and those presented here.

If you have alternative answers to the questions in this exercise, you are encouraged to post your answers and discuss them at the companion web site for this book, located at:

```
http://www.phptr.com/phptrinteractive/
```

### 5.2.1 ANSWERS

- * What is the purpose of the double dash (--) on line 5051?
  Answer:It marks the end of the options to the set command, and the beginning of the parameters for it.

If the double dash were missing, set would interpret -vu and -do as its own options, and you would get an error message because -d is not a valid option for set.

- * What would be output if you printed a reference to the special variables # and @ between lines 5051 and 5052?
  Answer:You would see the number 3 and the values of the three parameters, like the following interaction:
  [5051a] print $#: $@
  3: -vu -do hello

There are options, but the user chose to write them as two parameters. The third parameter doesn't start with a dash, so it does not contain any options.
