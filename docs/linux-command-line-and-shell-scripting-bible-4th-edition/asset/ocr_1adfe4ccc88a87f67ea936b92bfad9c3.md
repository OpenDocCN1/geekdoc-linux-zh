```
```
$
```
```

This example uses the unset command to remove the value at index value 2. When you display the array, it appears that the other index values just dropped down one. However, if you specifically display the data at index value 2, you see that that location is empty.

You can remove the entire array just by using the array name in the unset command:

```
```
$ unset mytest
$ echo ${mytest[*]}
```

```

```
```
$
```
```

Sometimes variable arrays just complicate matters, so they're often not used in shell script programming. They're not very portable to other shell environments, which is a downside if you do lots of shell programming for different shells. Some Bash system environment variables use arrays (such as BASH_VERSIONINFO), but overall you probably won't run into them very often.

# ## Summary

This chapter examined the world of Linux environment variables. Global environment variables can be accessed from any child shell spawned by the parent shell in which they're defined. Local environment variables can be accessed only from the process in which they're defined.

The Linux system uses both global and local environment variables to store information about the system environment. You can access this information from the shell command-line interface, as well as within shell scripts. The Bash shell uses the system environment variables defined in the original Unix Bourne shell, as well as lots of new environment variables. The PATH environment variable defines the search pattern the Bash shell takes to find an executable command. You can modify the PATH environment variable to add your own directories.

You can also create global and local environment variables for your