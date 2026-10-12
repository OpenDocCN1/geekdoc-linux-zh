Or it can be a multiline comment that starts with /* and ends with */. For example:

```
/*
    This is a multiline comment in named.conf
*/
```

Apart from the comments and blank lines, which are ignored by named, the real configuration lines are called statements, which have the following syntax:

```
keyword {
    // details of the statement
};
```

named can make use of many types of statements. I will discuss only the most commonly used here.

# Options statement

The options statement enables you to set up global options for the name server. You should use only a single options statement in the named.conf file. If no options statement is specified, a default options statement with each option set to its default is used. Many options can go inside the options statement block, enclosed by the {}. The commonly used options are as follows:

```
options {
    directory path_name;
    statistics-interval number;
    forwarders { [ in_addr ; [ in_addr ; ... ] ] };
    forward ( only | first );
};
```

The directory option enables you to specify the working directory path of the name server. If a directory is not specified, the working directory defaults to “.”, the directory from which the server was started. The directory specified should be an absolute path. Also note that when you specify