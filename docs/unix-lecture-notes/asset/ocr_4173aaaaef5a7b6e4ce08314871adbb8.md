much ignores argv[0] and only starts paying attention to arguments starting with argv[1]. This is not the best way to use execve() – it only works in a few circumstances.

Are you wondering about the printf() after the call? The printf() statement will only be executed if the execve() call fails; the only reason that execve() returns is failure to execute the program.

The next program, execvedemo2.c, uses execve() to execute the first command line argument of the program, passing to it the remaining arguments from the command line. In other words, if we supply a line like

```
$ execvedemo2 /bin/ls -l ..
```

it will execute it as if you typed the /bin/ls -l .. on a line by itself.

# Listing 7.8: execvedemo2.c

```
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

int main (int argc, char * argv[], char * envp[])
{
    if (argc < 2) {
        fprintf(stderr, "Usage: %s program args\n", argv[0]);
        exit (1);
    }
    execve(argv[1], argv+1, envp);
    fprintf(stderr,"execve() failed to run.\n");
    exit(1);
}
```

Notice that it uses pointer arithmetic to pass the array argv[1 .. argc-1] rather than argv[0 .. argc-1].

# 7.8.2 The exec() Library Functions

Because it is a little inconvenient to arrange everything for execve(), the designers of UNIX created a family of five functions that act as front-ends to execve(), each expecting a different set of parameters. They are

```
#include <unistd.h>
extern char **environ;

int execl(const char *path, const char *arg, ...);
int execIp(const char *file, const char *arg, ...);
int execle(const char *path, const char *arg, ..., char* const envp[]);
int execv(const char *path, char * const argv[]);
int execvp(const char *file, char * const argv[]);
```

Each of these contains either an 'l' or a 'v' in its name. The versions that contain an 'l', execl(), execlp() and execle(), expect a null-terminated list of null-terminated string arguments whereas