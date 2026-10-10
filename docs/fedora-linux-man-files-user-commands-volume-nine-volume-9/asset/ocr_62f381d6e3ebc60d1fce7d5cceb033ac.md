# DESCRIPTION

Rdist is a program to maintain identical copies of files over multiple hosts. It preserves the owner, group, mode, and mti of files if possible and can update programs that are executing. Rdist reads commands from *distfile* to direct the updating of files and/or directories. If *distfile* is `'-'`, the standard input is used. If no *-f* option is present, the program looks first for `Distfile`, then `Distfile` to use as the input. If no nas are specified on the command line, *rdist* will update all of the files and directories listed in *distfile*. Otherwise, the argument is taken to be the na of a file to be updated or the label of a command to execute. If label and file nas conflict, it is assud to be a label. These may be used together to update specific files using specific commands.

The *-c* option forces *rdist* to interpret the remaining arguts as a small *distfile*. The equivalent distfile is as follows. `( na …. ) -> [login@]host install [dest] ;`

The *-Server* option is recognized to provide partial backward compatible support for older versions of *rdist* which used this option to put *rdist* into server mode. If *rdist* is started with the *-Server* command line option, it will attempt to exec (run) the old version of *rdist*. This option will only work if *rdist* was compiled with the location of the old rdist (the path `/usr/bin/olddist` is used on Red Hat linux) and that program is available at run ti.

Rdist can use either the `(3)` function call or run an arbitrary transport program such as `(1c)` to access each target host. The thod used is selected at compile-ti. However, if the later thod is used, the transport program can be specified at run-ti on the command line with the default being `(1c)`. If the `(1c)` thod is used and the target host is the string **localhost** and the remote user na is the sa as the local user na, *rdist* will run the command

```
```sh
/bin/sh -c rdistd -S
```
```

Otherwise *rdist* run will run the command

```
```sh
rsh host -l reser rdistd -S
```
```

where *host* is the na of the target host, *reser* is the na of the user to make the connection as and, *rdistd* is the rdist server command on the target host as shown below. To use a transport program other than `(1c)` use the *-P* option. Whatever transport program is used, st be compatible with the above specified syntax for `(1c)`. If the transport program is not, it should be *wrapped* in a shell script which does understand this command line syntax and which then executes the real transport program.

Here's an example which uses `(1)` as the transport:

```
```sh
rdist -P /usr/local/bin/sh -f myDistfile
```
```

If the `(3)` thod is used, then *rdist* makes the connection to the target host itself and runs the *rdistd* server program as shown below. The default, and preferred thod, is to use `(1c)` to make the connection to target hosts. This allows *rdist* to be run without being setup to “root”.