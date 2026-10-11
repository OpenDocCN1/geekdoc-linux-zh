```
#include <unistd.h>
int execve(const char *filename, char *const argv[], char *const envp[]);
```

```
int exec l(const char *path, const char *arg, ...);
int execlp(const char *file, const char *arg, ...);
int execle(const char *path, const char *arg, ..., char *const envp[]);
int execv(const char *path, char *const argv[]);
int execvp(const char *file, char *const argv[]);
```

We refer to these functions as the “exec() family.” There is no function named exec(); instead we use this function name to mean any of the above listed functions. As with fork(), “exec” is used in Unix parlance as a verb, meaning to execute (run) a program, and as a noun.

# 9.1.4.1 The execve() System Call

The simplest function to explain is execve(). It is also the underlying system call. The others are wrapper functions, as is explained shortly.

```
int execve(const char *filename, char *const argv[], char *const envp[])
```

filename is the name of a program to execute. It may be a full or relative pathname. The file must be in an executable format that the kernel understands. Modern systems uses the ELF (Extensible Linking Format) executable format. GNU/Linux understands ELF and several others. Interpreted scripts can be executed with execve() if they use the '#'! ' special first line that names the interpreter to use. (Scripts that don’t start with “#!” will fail.) Section 1.1.3, “Executable Files,” page 7, provides an example use of “#!”.

argv is a standard C argument list—an array of character pointers to argument strings, including the value to use for argv[0], terminated with a NULL pointer.

envp is the environment to use for the new process, with the same layout as the environ global variable (see Section 2.4, “The Environment,” page 40). In the new program, this environment becomes the initial value of environ.

A call to exec() should not return. If it does, there was a problem. Most commonly, either the requested program doesn’t exist, or it exists but it isn’t executable (ENOENT and EACCES for errno, respectively). Many more things can go wrong; see the execve(2) manpage.