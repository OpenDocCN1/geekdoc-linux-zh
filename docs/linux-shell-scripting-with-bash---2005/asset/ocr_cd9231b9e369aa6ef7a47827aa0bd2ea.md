When using system to run a script, two shell sessions are created; one for *system* and another to run the script (unless the script is started with *execl*). To run scripts instead of shell commands, the C *popen* function is a less cumbersome method. *popen* runs a program and attaches a pipe to or from the program, as if the shell pipe operator | was used. The command has two parameters: the program to run and its arguments, and an *r* if the C program reads the standard output of the script, or a *w* if the program writes to the standard input of the script. When the program is finished, close the pipe with the *p close* command.

In the case of shell scripts, the program *popen* runs is Bash. You can rewrite the *c_system.c* program using *popen*, as shown in Listing 18.2.

# **Listing 18.2** c_popen.c

```
/** c_popen.c: run a Bash command from C using popen */
#include <stdio.h>
#include <stdlib.h>

int main() { 
    FILE *f = NULL;                  /* the pipe file */
    char s[ 255 ] = "";              /* a string buffer */

    f = popen( "/bin/bash -c \"ls -l *.txt\", "xr" ); /* open the pipe */
    while ( ! feof( f ) ) {         /* while more output */
        fgets( s, 255, f );         /* get the next line */
        printf( "%s", s );           /* print the results */
    }
    pclose( f );                     /* close the pipe */
    
    return 0;                        /* successful status */
}
```

The results are the same.

```
$ ./c_popen
company.txt
log.txt
orders.txt
temp.txt
```

If C variables are to be shared with a Bash script, they must be exported to the shell's environment. The C *putenv* function declares or changes an environment variable. The declaration should be in the same form as a Bash variable assignment. Because *putenv* increases the size of the environment, there is a chance it might fail. The command returns a zero if the assignment was successfully carried out.