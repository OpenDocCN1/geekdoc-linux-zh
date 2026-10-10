3.1. COMMAND LINE INTERFACE 51

# ### 3.1.2  Application Programs

The shells are not the only programs which process user commands. Application programs receive user commands via three paths: the command line, the environment, and the standard input. The command line and environment variables are used to pass information to the command which generally apply to the entire operation of the command. For example, the **sort** command can be told to treat upper and lower case characters as equal with the `-f` command line option and the **man** command can be provided a special search path via the **MANPATH** environment variable.

The processing of the standard input stream is much more specialized. The various text editors give proof of that.

# #### Command line parsing

One of the more unfortunate characteristics of Linux, Unix, and Unix-like systems is that each command seems to have a different syntax and meaning for command line options. This is a natural result of an underlying philosophy: the shell has no business interpreting command line arguments. As a consequence, each command applies its own syntax rules and, for a long time, used its own code to parse the command line. This approach has been changing over the last decade---ever since the **getopt** library routine was first offered.

The **getopt** routine formalized the convention that single-letter options have a leading “-” and that they may be grouped together provided that only the last one takes an additional argument. Long option names (as used by the **GNU** utilities) have a leading “--” and must stand alone in the command line. Anything past the last option is a general argument---a list of file names is a common example.

There still exist a number of commands which do not conform to this new syntax. This is for reasons of backward compatibility.

The meaning assigned to the options remains confused and is unlikely to change. Thus `-f` means *fold* for the **sort** command, *do not sort* for the **ls** command, *whatis* for the **man** command, etc.

The only hope in this respect is a move towards longer option names. Instead of relying on a single letter, options are being defined for longer