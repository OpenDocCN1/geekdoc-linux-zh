```
{
    char my_string[] = "hello there";
    
    my_print (my_string);
    my_print2 (my_string);
}

my_print (char *string)
{
    printf ("The string is %s\n", string);
}

my_print2 (char *string)
{
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

# ## Additional C Programming Tools

The Slackware Linux distribution includes a number of C development tools that have not yet been described. This section describes many of these additional tools and their typical uses.

# ### xxgdb

xxgdb is an X Window system-based graphical user interface to gdb. All of the features that exist in the command-line version of gdb are present in xxgdb. xxgdb enables you to perform many of the most commonly used gdb commands by pressing buttons instead of typing in commands. It also graphically represents where breakpoints have been placed.

Start xxgdb by typing the following into an Xterm window.

```
xxgdb
```

When we initiate xxgdb, we can specify any of the command-line options that were available with gdb. xxgdb also has some of its own command-line options. These are described in Table 26.2.