```
```
}
$ 
```
```

The next step is to include the myfuncs library file in your script files that want to use any of the functions. This is where things get tricky. The problem is with the scope of shell functions. As with environment variables, shell functions are valid only for the shell session in which you define them. If you run the myfuncs shell script from your shell command-line interface prompt, the shell creates a new shell and runs the script in that new shell. This defines the three functions for that shell, but when you try to run another script that uses those functions, they aren't available.

This applies to scripts as well. If you try to just run the library file as a regular script file, the functions don't appear in your script:

```
```
$ cat badtest4
#!/bin/bash
# using a library file the wrong way
./myfuncs

result=$(addem 10 15)
echo "The result is $result"
$
$ ./badtest4
./badtest4: addem: command not found
The result is
$ 
```
```

The key to using function libraries is the source command. The source command executes commands within the current shell context instead of creating a new shell to execute them. You use the source command to run the library file script inside your shell script. Doing so makes the functions available to the script.

The source command has a shortcut alias, called the dot operator. To source the myfuncs library file in a shell script, you just need to add the following line:

```
```
. ./myfuncs
```
```

This example assumes that the myfuncs library file is located in the same directory as the shell script. If not, you need to use the