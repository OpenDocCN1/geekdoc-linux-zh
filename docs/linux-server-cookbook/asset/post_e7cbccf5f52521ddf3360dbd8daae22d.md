
## Automation with shell scripting

A *shell script* is a program executed by the *Linux shell*. As the most popular *shell* historically is *bash*, it is also called *bash script*. The *script* contains different operations to be performed, such as running commands, setting variables, and showing text on the screen. Furthermore, the *script* can contain conditions and loops.

*Shell scripting* is the action of writing *shell scripts*. These scripts help to reduce repetitive tasks in the systems, and it helps to create logic during the execution. The *file* containing the operations usually has a ".sh" file extension. The *scripts* require to have execution permission to be executed or can be evoked through the commands *sh*, *bash*, or another *shell* command (*zsh*, *csh*, or *ash*).

A *shell script* can call to commands available in the system or to *builtin functions* provided by the *shell*. The following code shows a simple example using the *builtin function* called *read* and the Linux command *echo*.

```sh
#!/bin/sh
read  -p "What is your name? " NAME
echo  "Your name is: $NAME"
```

The first line is called *shebang*, and it indicates which executable will interpret the code defined in the file. The second line asks the user to input data and sets the value in the variable named *NAME*. The third line shows the text on the screen as well as the value of the variable. *Figure 12.1* shows the execution and the output:

```sh
agonzalez@ubuntu:~$ chmod u+x example1.sh
agonzalez@ubuntu:~$ ./example1.sh
What is your name? Alberto Gonzalez
Your name is: Alberto Gonzalez
```

**Figure 12.1:** Simple shell script example

In a shell script, we can include a list of the commands to be executed, each in a separate line. It is also possible to use pipes, as discussed in this book, to use the output of one command as the input for another one. In the first example, the function **read** was used to set a variable from the input, but in most of the cases, the variables are going to be set with a fixed value or with the output from a command.

A variable can contain a string or any number type. It is simple to define a variable: set the name of the variable desired, followed by an equal symbol (=) and the value desired. The name of the variable can be in uppercase (recommended for readability), lowercase, or combined. In case the value containing a text is separated by spaces, it is required to use double or simple quotes. The differences between the two options are as follows:

- Double quotes: it evaluates the value of the variables inside.
- Single quotes: treats the value between quotes as literal, without evaluation.

The following code shows how to set two variables and run three different commands with the variables.

```sh
#!/bin/sh

VARIABLE1=3.14

variable2="PI number is $VARIABLE1"

echo "The number PI is $VARIABLE1"

echo "Content of variable2: $variable2"

echo 'Content of variable2: $variable2'
```

The execution of the previous code is shown in *figure 12.2*, where the difference between double and single quotes is demonstrated. Moreover, a variable can contain another variable, as demonstrated in the variable named variable2:

```sh
agonzalez@ubuntu:~$ ./example2.sh
The number PI is 3.14
Content of variable2: PI number is 3.14
Content of variable2: $variable2
```

![](img/863afa537de4eed7deb11978bfbfa90e_372_0.png)

As described previously, a variable can set the value with the value of the output from one command. To execute a command and to be able to use the output, the syntax used for the command should be `$(command)`. The legacy syntax for running commands and obtaining the output was using `backticks`, such as “`command`”. This legacy syntax should be avoided in modern scripts. The following code shows how to set a variable with the output of one command and how to use the syntax `$( )` inside another command.

```sh
#!/bin/sh
NOW=$(date)
HOURS=5
echo "The date output is: $NOW"
echo "There are $(who | wc -l) users connected"
```

*Figure 12.3* shows the output example for the previous example, where the output for commands *date* and *uptime* are used.

```sh
agonzalez@ubuntu:~$ ./example3.sh
The date output is: Sun Oct 23 04:13:10 PM UTC 2022
There are 3 users connected
```

![](img/863afa537de4eed7deb11978bfbfa90e_372_1.png)

In a *shell script*, the same concepts described in *Chapter 3, Using the Command Line*, are applied to the scripts. Special characters and escape characters are treated the same, as indicated in that chapter. Inside the program, there are some special variables that can be used. *Table 12.1* lists some of the most used:

| Variable | Description |
| :--- | :--- |
| `$0` | The name of the program file. |
| `$1, $2, $n` | The first, second, or the *n* argument from the invocation. |
| `$#` | The number of arguments supplied to the program. |
| `$@` | All the arguments passed are treated as one string. |
| `$?` | The exit status (-1, 0, or a positive number) from the previous command executed. |
| `$$` | The current process ID for the script. |

**Table 12.1:** Special variables in a shell script.

The following code shows a *script* example using all the special variables.

```sh
#!/bin/sh
echo "The name of the script is $0"
echo "The number of the arguments are $#"
echo "The first argument value is $1"
echo "The second argument value is $2"
echo "The value for all arguments are: $@"
echo "The current process id is $$"
uptime
echo "The exit status for the command uptime was $?"
notexisting
echo "The exit status for the command notexisting was $?"
```

*Figure 12.4* shows an example output when three arguments are passed to the script with the name **example4.sh**:

```sh
agonzalez@ubuntu:~$ ./example4.sh alberto gonzalez rodriguez
The name of the script is ./example4.sh
The number of the arguments are 3
The first argument value is alberto
The second argument value is gonzalez
The value for all arguments are: alberto gonzalez rodriguez
The current process id is 17247
  15:16:59 up 21:00,  1 user,  load average: 0.00, 0.00, 0.00
The exit status for the command uptime was 0
./example4.sh: 10: notexisting: not found
The exit status for the command notexisting was 127
```

**Figure 12.4:** Using special variables on a shell script

One of the biggest advantages of using a *shell script* is the possibility to use conditions. Conditions will allow the application to take decisions depending on variables or different expressions indicated. The syntax for the following condition decisions is as follows:

- **if/else** statement: It evaluates the expression indicated in the *if*, and if true, it will execute the operations indicated inside. If the expression is *false*, then it will execute the instructions inside the *else* block. The syntax is the following:
  ```text
  if EXPRESSION; then
      if_statements
  else
      else_statements
  fi
  ```

- **if/elif/else** statement: Same as the previous one, but the element **elif** evaluates a different expression than the *if*. The syntax is as follows, and it can contain several **elif** elements:
  ```text
  if EXPRESSION; then
      if_statements
  elif EXPRESSION2; then
      elif_statements1
  elif EXPRESSION3; then
      elif_statements2
  else
      else_statements
  fi
  ```

- **case/esac statement:** It evaluates an expression, and it matches different patterns defined. If one pattern matches, the statements defined will be executed. The syntax is the following:
  ```text
  case EXPRESSION in
  PATTERN_1)
      STATEMENTS
      ;;
  PATTERN_2)
      STATEMENTS
      ;;
  *)
      STATEMENTS
      ;;
  esac
  ```

The `expression` to be evaluated as a condition is based on the available expressions for the `builtin function` named `test`. The expression can be wrapped using square brackets ([ and ]) or after the word `test`. The following code shows an equivalent example with both syntaxes:

```sh
if [ $# -ne 1 ]; then
    echo "Number of arguments should be one"
fi

if test $# -ne 1; then
    echo "Number of arguments should be one"
fi
```

The `expressions` are used to check and make comparisons. In the previous code, the check `-ne` stands for *not equal*. The most used checks and comparisons available and their respective descriptions are shown in *table 12.2*:

| Check | Description |
| :--- | :--- |
| -n STRING | The length of *STRING* is nonzero |
