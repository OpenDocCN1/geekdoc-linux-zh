Several options can be specified on each line after the hostname. The options are separated by white space.

+   **lo= username** allows you to specify another login name for this host; otherwise, your login name on the startup machine is used.

+   **so= pw** causes PVM to prompt you for a password on this host. This is useful when you have a different user_id and password on a remote system. PVM uses **rsh** by default to start up remote **pvmds**, but when **pw** is specified, PVM will use **rexec()** instead.

+   **dx= location of pvmd** allows you to specify a location other than the default for this host. This is useful if you wish to use your own copy of pvmd.

+   **ep= paths to user executables** allows you to specify a series of paths to search down to find the requested files to spawn on this host. Multiple paths are separated by a colon.

+   **sp= value** specifies the relative computational speed of the host compared with other hosts in the configuration. The range of possible values is 1 to 1,000,000, with 1,000 as the default.

+   **bx= location of debugger** specifies which debugger script to invoke on this host if debugging is requested in the spawn routine. Note that the environment variable PVM_DEBUGGER can also be set.

+   **wd= working_directory** specifies a working directory in which all spawned tasks on this host will execute. The default is **$HOME**.

+   **so= ms** specifies that a slave **pvm** will be started manually on this host. This is useful if **rsh** and **rexec** network services are disabled but IP connectivity exists. When using this option you will see the following in the tty of the pvmd3:

```
```text
[t80040000] ready     Fri Aug 27 18:47:47 1993
*** Manual startup ***
Login to "honk" and type:

pvm3/lib/pvmd -S -d0 -rhonk 1 80a95c43:0c6 4096 2 80a95c43:0000
Type response:
```
```

On **honk**, after typing the given line, you should see

```
```text
d6pro<2312> arch<ALPHA>  ip<80a95c43:0a8e> mtu<4096>
```
```