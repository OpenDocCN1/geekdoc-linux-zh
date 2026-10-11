# ### Configuring man page access

As was mentioned earlier in the chapter, the `usr/man` directory is the default location for man page source files. The `MANPATH` environment variable can be used to change the default search path for man page source files. The `MANPATH` variable will overwrite the default search path for man pages, so including the path to existing man pages, if they will be needed, is important. Below is an example of a `MANPATH` variable setting added to a `/home/user/.profile` file.

```
Export MANPATH=/usr/local/man:/usr/man:/prefomat::/usr/man:/usr/X11R6/man
```

Most of the documents stored in `usr/man` are compressed and unformatted. The man command uses the `/etc/man.config` file for information on the proper display of these files. This file contains `MANPATH` information as well as compression, formatting, and pager settings. Using the option -C shown in Table 7-1, a different configuration file can be specified.

The man command is located in `/usr/bin`. This directory needs to be located in the `PATH` environment variable, or the command must be run using the absolute path `/usr/bin/man`.

# ## Using Documentation Stored in /usr/doc

+   * **Use and Manage Local System Documentation.** Use and administer the man facility and the material in `/usr/doc/.` Includes finding relevant man pages, searching man page sections, finding commands and man pages related to one, configuring access to man sources and the man system, using system documentation stored in `/usr/doc/` and related places, determining what documentation to keep in `/usr/doc/`.

Along with the man pages, a variety of other documentation can be stored on the local system. Table 7-3 shows some common locations of documentation and the data stored there.

| **Table 7-3** | **Documentation Locations** |
| Location | Documentation |
| /usr/doc/program_name | Documentation for program_name |
| /usr/doc/FAQ | Frequently Asked Questions |