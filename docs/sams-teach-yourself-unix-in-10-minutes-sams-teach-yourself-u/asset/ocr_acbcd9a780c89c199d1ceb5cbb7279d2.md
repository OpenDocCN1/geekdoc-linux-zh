# Shells and Executable Files

Technically, it doesn’t even search these locations when you try to execute a program. The shell actually keeps a catalog of all the executable files found in these locations. If a new executable appears in one of these locations while you’re logged in, your shells won’t know about it until you execute the rehash command, which asks the shell to go back and rebuild the catalog.

You might notice that if you have a copy of a program in your current directory, in some cases typing the filename results in a command not found error. This is because it’s common for the path variable to lack the current directory. You can either execute programs in the current directory by typing ./<programname> or by adding the current directory to your path.

# Working with Paths

The current directory is usually left out of the path because including it is a bit of a security risk. If the current directory is in your path, you can potentially be fooled into executing arbitrary programs by naming them as common UNIX commands and sneaking them into your directories. If you want to put the current directory in your path, always put it at the end of the path. That way normal UNIX commands will be found before any Trojan horses that might have made their way into your system.

If you want to see what your current path is, you can do so by using echo $path. If it’s missing some paths you need, for instance the current directory and /usr/local/bin, you can add these by using the following command:

```
set path=( $path /usr/local/bin . )
```