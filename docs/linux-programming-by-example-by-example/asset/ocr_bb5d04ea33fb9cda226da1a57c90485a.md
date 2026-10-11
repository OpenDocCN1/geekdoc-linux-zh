# # Example

![](bbox=[0.04, 0.12, 0.1, 0.18])

# ## Example

This sample makefile will make the discussion more concrete. It is the makefile for building a text editor imaginatively named editor.

```
```text
# Makefile.1
#

clean:
	rm editor *.o
```
```make
editor: editor.o screen.o keyboard.o
	gcc -o editor editor.o screen.o keyboard.o

editor.o: editor.c editor.h keyboard.h screen.h
	gcc -c editor.c

screen.o: screen.c screen.h
	gcc -c screen.c

keyboard.o: keyboard.c keyboard.h
	gcc -c keyboard.c
```
```

To compile *editor*, you would simply type *make* in the directory containing the makefile. It's that simple.

This makefile has *five* rules. The first target, *editor*, is called the *default* target—this is the file that *make* ultimately tries to create. *editor* has three dependencies, *editor.o*, *screen.o*, and *keyboard.o*; these three files must exist in order to build *editor*. The next line is the command that *make* executes to create *editor*. As you recall from Chapter 1, "Compiling Programs," this compiler invocation builds an executable named *editor* from the three object modules, *editor.o*, *screen.o*, and *keyboard.o*. The next three rules tell *make* how to build the individual object modules.

Here is where *make*'s value becomes evident: ordinarily, if you tried to build *editor* using the command from line 2, *gcc* would complain loudly and quit if the dependencies did not exist. *make*, on the other hand, after determining that *editor* requires these files, first verifies that they exist and, if they do not, executes the commands to create them. Then it returns to the first rule to create the *editor* executable. Of course, if the dependencies for the components, *keyboard.c* or *screen.h*, don't exist, *make* will also give up, because it lacks targets named, in this case, *keyboard.c* and *screen.h*.