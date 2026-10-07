# TIP

You can specify different kinds of dependencies for a target by placing the same target name on different dependency lines. Actually, make is even more powerful than described in this chapter, but unless you are working on very large projects with lots of interdependencies, you probably won't care about most of the subtleties make is capable of.

The first entry in our makefile is the key one for building our executable. It states that someonenappy is to be built if all the dependent object files and library files are present and if there are any newer files than the last version of someonenappy. Of course, if the executable is not present at all, make performs the compile command listed, but not right away. First, make checks to see which object files need to be recompiled in order to recompile someonenappy. This is a recursive operation, as make examines the dependencies of each target in the hierarchy, as defined in the makefile.

The last entry is a little goofy. It copies the header files yes.h and no.h (somehow related to maybe.h) to the home directories of the user named sue if they have been modified. This is somewhat conceivable if Sue is working on related programs that use these header files and need the most recent copies at all times. More importantly, it illustrates that make can be used to do more than compiling and linking and that make can execute several commands based on one dependency.

The fresh target is another example of a target being used to do more than just compiling. This target lacks any dependents, which is perfectly acceptable to the make program. As long as there is no file in the current directory named fresh, make executes the supplied command to remove all object files. This works because make treats any such entry as a target that must be updated.

So, if you enter the command

```
$ make someonenappy
```

make starts issuing the commands it finds in the makefile for each target that must be updated to achieve the final target. make echoes these commands to the user as it processes them. Simply entering

```
$ make
```

also works in this case because make always processes the first entry it finds in the makefile. These commands are echoed to the screen, and the make process halts if the compiler finds an error in the code.