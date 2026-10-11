```
{
    void *handle;
    void (*errfcn)(); /* pointer to the loaded code to use */
    const char *errmsg;
    FILE *pf;
```

```
/* Load the object of our desire */
    handle = dlopen("liberr.so", RTLD_NOW);
    if (handle == NULL) {
        printf("failed to load liberr.so: %s\n", dlerror());
        exit(EXIT_FAILURE);
    }
```

```
/* Clear the error string, if any */
    dlerror();
    errfcn = dlsym(handle, "err_ret");
    if ((errmsg = dlerror()) != NULL) {
        printf("didn't find err_ret(): %s\n", errmsg);
        exit(EXIT_FAILURE);
    }
```

```
/* Now use the loaded symbol, err_ret */
    if ((pf = fopen("foobar", "r")) == NULL)
        errfcn("couldn't open foobar");
```

```
/* Be a good citizen and unload the object */
    dlclose(handle);
    exit(EXIT_SUCCESS);
}
```

![](bbox=[0.04, 0.59, 0.15, 0.63])

# Output

```
$ gcc -g -Wall dltest.c -o dltest -ldl
$ LD_LIBRARY_PATH=$(pwd) ./dltest
couldn't open foobar: No such file or directory
```

As you can see, you do not have to link against liberr or include liberr.h in the source code. All access to liberr.so comes through the dl interface. dltest’s use of the dlerror call illustrates the correct way to use it. Call dlerror once to reset the error string to NULL, call dlsym, and then call dlerror again to save its return value in another variable so you can use the string later. Call errfcn as you normally would call the function to which it points. Finally, unload the shared object and exit.