Just as most Linux commands accept command line options, a **bash** script also accepts command line options. Inside the script, you can refer to the options as $1, $2, and so on. The special name $0 refers to the name of the script itself.

To run this shell script, first you have to make the file executable (that is, turn it into a program) with the following command:

```
chmod +x simple
```

Now type ./simple one two to run the script, and it displays the following output:

```
This script's name is: ./simple
Argument 1: one
Argument 2: two
```

The . / prefix to the script's name indicates that the simple file is in the current directory.

This script simply prints the script's name and the first two command line options that the user types after the script's name.

Next, try running the script with a few arguments, as follows:

```
./simple "This is one argument" second-argument third
This script's name is: ./simple
Argument 1: This is one argument
Argument 2: second-argument
```

The shell treats the entire string within the double quotation marks as a single argument. Otherwise, the shell uses spaces as separators between arguments on the command line.

Most useful shell scripts are more complicated than this simple script, but this simple exercise gives you a rough idea of how to write shell scripts.

![](bbox=[0.14, 0.78, 0.23, 0.85])

Place Linux commands in a file and use the chmod command to make the file executable. Voilà! You created a shell script!