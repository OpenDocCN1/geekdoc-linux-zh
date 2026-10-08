```
```
.c.o:
	cc -c -O *.c

or:

.c.o:
	cc -c -O $<
```
```

$* The macro $* is the current target name with the suffix deleted. It is evaluated only for inference rules.

These five macros can have alternative forms. When an uppercase D or F is appended to any of the five macros, the meaning is changed to ``directory part'' for D and ``file part'' for F. Thus, $(@D) refers to the directory part of the string $@. If there is no directory part, ./ is generated. When the $? macro contains more than one dependent name, the $(?D) expands to a list of directory name parts and the $(?F) expands to a list of the filename parts.

In addition to the built-in macros listed above, other commonly used macros are defined by make. These macros are used in the default inference rules, and can be displayed with the -p option. These macros can be used in target rules in the makefile. They can also be redefined in the makefile.

$$@
The $$@ macro has meaning only on dependency lines. Macros of this form are called dynamic dependencies because they are evaluated at the time the dependency is actually processed. $$@ evaluates to exactly the same thing as @ does on a command line; i.e., the current target name. This macro is useful for building large numbers of executable files, each of which has only one source file. For instance, the following HP-UX commands could all be built using the same rule:

```
```
CMDS = cat echo cmp chown
$(CMDS) : $$@.c
	$(CC) -O $^ -o $$
```
```

If this makefile is invoked with make cat echo cmp chown, make builds each target in turn using the generic rule, with @ evaluating to cat while cat is the target, to echo when the target is echo, and so forth.

The dynamic dependency macro can also take the F form, $$(@F) which represents the filename part of $$. This is useful if the targets contain pathnames. For example:

```
```
INCDIR = /usr/include
INCLUDES = $(INCDIR)/stdio.h \
		$(INCDIR)/pwd.h \
		$(INCDIR)/dir.h \
		$(INCDIR)/a.out.h
$(INCLUDES) : $$(@F)
	cp $^ $$
	chmod 0444 $$
```
```

# Special Macros

The VPATH macro allows make to search a colon separated list of directories for dependents. Lines of the form VPATH= path1:path2 ... causes make to first search the current directory for a dependent and