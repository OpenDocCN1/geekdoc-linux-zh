He would see

```
. . Contineants Oceans
```

Similarly, if jack were to use this command with the pathname of jill's Marsupials directory, he would see something like this:

```
$ ls -a ../jill/Marsupials (Return)
```

```
. . bandicoot kangaroo wombat
```

Note that dot (. ) and dotdot (..) are both names of hidden directories, and that both appear when jack uses the ls -a command. Remember, dot is just another name for the current directory, while dotdot refers to the parent of the current directory.

# 5.8 Renaming and Moving Files

The ls command takes one pathname; now consider a command that uses two. The mv (“move”) command has the general form

```
mv pathname1 pathname2
```

This can be interpreted to mean “move the file found at pathname1 to the position specified by pathname2.” To see how this works, consider how jill might tidy up her home directory using mv.

The file name possum is wrong because the proper name for the animal is “opossum.” If jill is still working in her home directory, the pathname of the file possum is just the file name. To change the name of the file without changing its location, she simply uses mv with the new name:

```
$ mv possum opossum (Return)
```

This tells UNIX “move the contents of possum (in the current directory) into the file opossum (also in the current directory).” Since there is no existing opossum file, one is created, and the old file name disappears.

Next, jill remembers that the opossum is a marsupial, and therefore should be moved to the Marsupials directory. The mv command will do the trick:

```
$ mv opossum Marsupials (Return)
```

This means “move opossum from the current directory into the Marsupials directory.” Thus jill can use the mv command twice, once to rename a file and again to move it to another directory. The end result is shown in Figure 5-3.