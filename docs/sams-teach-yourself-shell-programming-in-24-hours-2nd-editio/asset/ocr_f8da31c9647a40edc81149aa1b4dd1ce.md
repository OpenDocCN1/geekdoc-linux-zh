The output is similar to the following:

```
root /
daemon /
bin /usr/bin
sys /
adm /var/adm
ranga /home/ranga
```

# Allowing awk to Use Shell Variables

Most versions of awk have no direct way of accessing the values of environment variables set by the shell. In order for awk to use these variables, you have to convert them to awk variables on the command line as follows:

```
awk 'script' awkvar1=value awkvar2=value ... files
```

Here, script is the awk script that you want to execute. The variables awkvar1, awkvar2, and so on are the names of awk variables that you want to set. As usual, files is a list of files.

Let's say that you want to generate a list of all the fruits in fruit_prices.txt that are less than or equal to some number x, where x is supplied by the user. In order to make this possible, we need to forward the value of x given by the user to awk. Assuming that the user-supplied value of x is available in the shell variable $1, the script is

```
#!/bin/sh
NUMFRUIT="$1"
if [ -z "$NUMFRUIT" ] ; then NUMFRUIT=75 ; fi
awk '
$3 <= numfruit { print ; }
' numfruit="$NUMFRUIT" fruit_prices.txt
```

Only those lines that have less than the specified number of fruit are printed.

Assuming this script is called reorder_user.sh and is located in the current directory, it can be executed as follows:

```
$ ./reorder_user.sh 25
```

This produces the output

```
Kiwi    $1.50    22
```

# Flow Control

There are three main forms for flow control in awk:

+   - The if statement
+   - The while statement
+   - The for statement