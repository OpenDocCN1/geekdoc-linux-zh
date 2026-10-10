```
```
    for (counter = 0; counter < 100; counter++)
        printf ("\nValue of element %d is %d",counter,array[counter]);
}
```
```

# Passing Parameters to main()

C allows parameters to be passed from the operating system to the program when it starts executing through two parameters, *argc* and *argv[ ]*, as follows:

```
```
#include <stdio.h>

main(int argc, char *argv[ ])
{
    int n;
    for (n = 0; n < argc; n++)
        printf ("\nParameter %d equals %s",n,argv[n]);
}
```
```

The parameter *argc* holds the number of parameters passed to the program; and the array *argv[ ]* holds the addresses of each parameter passed; *argv[0]* is always the program name. This feature may be put to good use in applications that need to access system files. Consider the following scenario: A simple database application stores its data in a single file called *data.dat*. The application needs to be created so that it may be stored in any directory on either a floppy diskette or a hard disk, and executed both from within the host directory and through a DOS search path. To work correctly, the application must always know where to find the data file *data.dat*. This can be solved by assuming that the data file will be in the same directory as the executable module, a not unreasonable restriction to place upon the operator. The following code fragment illustrates how an application may apply this algorithm to be always able to locate a desired system file:

```
```
#include <string.h>

char system_file_name[160];

void main(int argc,char *argv[ ])
{
    char *data_file = "DATA.DAT";
    char *p;

    strcpy(system_file_name,argv[0]);
    p = strstr(system_file_name,".EXE");
    if (p == NULL)
    {
        /* The executable is a .COM file */
        p = strstr(system_file_name,".COM");
    }

    /* Now back track to the last '\' character in the file name */
    while (*(p - 1) != '\\')
        p--;
```
```

235