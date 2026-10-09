Most UNIX users are familiar with the *nice* *command*, which runs a program at a lower priority (or a higher one if run by a superuser). Here’s our version:

```
```c
#define USAGE "usage: aupnice [-num] command\n"

int main(int argc, char *argv[])\n{
  int incr, cmdarg;
  char *cmdname, *cmdpath;

  if (argc < 2) {
    fprintf(stderr, USAGE);
    exit(EXIT_FAILURE);
  }
  if (argv[1][0] == '-') {
    incr = atoi(&argv[1][1]);
    cmdarg = 2;
  }
  else {
    incr = 10;
    cmdarg = 1;
  }
  if (cmdarg >= argc) {
    fprintf(stderr, USAGE);
    exit(EXIT_FAILURE);
  }
  (void)nice(incr);
  cmdname = strchr(argv[cmdarg], '/');
  if (cmdname == NULL)
    cmdname = argv[cmdarg];
  else
    cmdname++;
  cmdpath = argv[cmdarg];
  argv[cmdarg] = cmdname;
  execvp(cmdpath, &argv[cmdarg]);
  EC_FAIL

  EC_CLEANUP_BGN
  exit(EXIT_FAILURE);
  EC_CLEANUP_END
}
```
```

Note how we reuse the incoming *argv* in the call to *execvp*. The variable *cmdarg* holds the subscript of the command path (either 1 or 2, depending on whether an increment was specified). That part of *argv* starting with *cmdarg* is the part to be passed on. You might want to contrast this with the more extensive