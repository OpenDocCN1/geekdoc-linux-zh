```
```makefile
% cat makefile
CC = cc
OPTIONS = -O4 -o
OBJECTS = main.o input.o compute.o
SOURCES = main.c input.c compute.c
HEADERS = main.h input.h compute.h

power:
    main.c $(OBJECTS) -lm

main.o: main.c main.h input.h compute.h
input.o: input.c input.h
compute.o: compute.c compute.h

all.tar: $(SOURCES) $(HEADERS) makefile
    tar cvf - $(SOURCES) $(HEADERS) makefile > all.tar

clean:
    rm *.o
```
```

When the make command is executed, the commands for the last two targets (all.tar and clean) are not executed, as these targets do not depend on anything and nothing depends on them. You can invoke the commands associated with these targets by passing the targets as parameters to make. The advantage of putting these rules in the makefile is that you do not have to remember which files to archive (by using the tar command in this case) and which to remove once the final executable has been created. The make clean command invokes the rm *.o command to remove all object files that are created in the process of creating the executable for the software. The following session shows the output of make when executed with two targets as command line arguments. The tar archive is placed in the all.tar file.

```
```
% make all.tar clean
tar cvf - main.c input.c compute.c main.h input.h compute.h makefile > all.tar
a main.c
a input.c
a compute.c
a main.h
a input.h
a compute.h
a makefile
rm *.o
```
```

In the following in-chapter exercise, you will run the previous sessions on your system to further enhance your understanding of the make utility.