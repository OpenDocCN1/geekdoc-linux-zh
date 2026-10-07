```
char *string2;
int size, size2, i;

size = strlen (string);
size2 = size -1;
string2 = (char *) malloc (size + 1);
for (i = 0; i < size; i++)
    string2[size2 - i] = string[i];
string2[size] = '\0';
printf ("The string printed backward is %s\n", string2);
}
```

This generates the following output:

![](bbox=[0.14, 0.32, 0.48, 0.45])

calls recognizes a number of command-line options that enable you to specify the appearance of the output and which function calls get displayed. For more information on these command-line options, refer to the calls man page or enter calls -h at the command line.

# ## cproto

cproto is another program that is not included on this Linux CD-ROM but is readily available from FTP and BBS sites. cproto reads in C source files and automatically generates function prototypes for all of the functions. Using cproto saves you from having to type in a function definition for all of the functions that you have written in your programs.

> > ### TIP
>
> To install cproto on your system, perform the following steps while you are logged in as root:
> 1. Uncompress and untar the file.
> 2. cd into the cproto subdirectory created as a result of the untar command.
> 3. Move the file named cproto to the /usr/bin directory.
> 4. Move the file named cproto.1 to the /usr/man/man1 directory.
> 5. Remove the /tmp/cproto directory.
>
> This installs the cproto program and man page on your system.