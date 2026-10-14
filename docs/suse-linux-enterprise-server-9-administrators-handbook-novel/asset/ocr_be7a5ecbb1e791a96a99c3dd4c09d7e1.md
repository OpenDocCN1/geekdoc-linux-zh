You initiate transitions between states by running the init routine followed by the runlevel. Each transition, in turn, changes which processes are running. The application startups or shutdowns triggered by a change in the runlevel are managed through a series of script files. The directory `/etc/init.d` is the base directory for a collection of directories, each of which represents a distinct runlevel. Within each level's directory resides a collection of appropriate scripts for the applications required for the specific runlevel.

When the system enters a particular state, it initiates all the appropriate routines for that state by executing all the script files that begin with the letter S (Start) in the corresponding directory.

Similarly, when the system is leaving a source level for another, the scripts residing in the source directory beginning with the letter K (Kill) are processed. This ensures that all applications that are supposed to run only in a particular level are shut down properly before the system moves onto the next runlevel.

The one exception is one of efficiency. If a start script for a specific application exists in the target level, the stop (Kill) script in the source level is ignored.

As an example, you can examine the change of state from runlevel 3 and runlevel 5 on the xdm application. Xdm is the X Windows System display manager. Referring to Table 3.1, X is available at runlevel 5. Listing 3.3 show the files associated with xdm in the `/etc/init.d/rc5.d` directory.

# **LISTING 3.3**

xdm Files Associated with Runlevel 5

```
Castor:/etc/init.d # ls -l rc5.d | grep -e xdm
lrwxrwxrwx 1 root root 6 Jan 5 04:53 K06xdm -> ../xdm
lrwxrwxrwx 1 root root 6 Jan 5 04:53 S16xdm -> ../xdm
Castor:/etc/init.d #
```

From Listing 3.3, it is possible to see that xdm is both started and stopped as the system enters or leaves runlevel 5. What is also apparent is that both the startup and shutdown scripts are simply links to the same script residing in `/etc/init.d`. This linking minimizes duplication of the scripts, ensuring a consistent application startup and shutdown independent of target runlevel.

The init process can therefore be defined as a tool used to control which applications are active on a system. You can identify which applications are active within a runlevel by looking at content of the subdirectory for the level in question.