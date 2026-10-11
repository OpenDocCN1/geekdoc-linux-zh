# TABLE 2.1

Values for has_arg

| Symbolic constant | Numeric value | Meaning |
| :--------------- | :------------ | :------ |
| no_argument       | 0             | The option does not take an argument. |
| required_argument | 1             | The option requires an argument. |
| optional_argument | 2             | The option’s argument is optional. |


The use of flag and val seems confusing at first encounter. Let’s step back for a moment and examine why it works the way it does. Most of the time, option processing consists of setting different flag variables when different option letters are seen, like so:

```
while ( (c = getopt(argc, argv, "af: hv")) != -1) {
    switch (c) {
    case 'a':
        do_all = 1;
        break;
    case 'f':
        myfile = optarg;
        break;
    case 'h':
        do_help = 1;
        break;
    case 'v':
        do_verbose = 1;
        break;
    ...               Error handling code here
    }
}

```

When flag is not NULL, getopt_long() sets the variable for you. This reduces the three cases in the previous switch to one case. Here is an example long options table and the code to go with it:

```
int do_all, do_help, do_verbose;    /* flag variables */
char *myfile;

struct option longopt[] = {
    { "all",  no_argument,    & do_all,      1 },
    { "file", required_argument, NULL,       'f' },
    { "help", no_argument,    & do_help,     1 },
    { "verbose", no_argument,  & do_verbose,  1 },
    { 0, 0, 0, 0 }
};
...

```