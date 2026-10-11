![](bbox=[0.12, 0.05, 0.15, 0.06])

# LISTING 7.8  Creating Pipes in a Parent Process

```
```c
/***** Parent Process *****/
int FDs[2];     /* create the place holder for the new pipe */
pipe(FDs); /* create the pipe: FDs[0]=input, FDs[1]=output */
char buffer[1024];

/*---Create the process using fork() ---*/
close(FDs[0]);    /* Make write-only */
...
write(FDs[1], buffer, buffer_len); /* send message to child */
...
/*---do processing---*/
wait();
close(FDs[1]);
```
```

# LISTING 7.9  Creating Pipes in a Parent Thread

```
```c
/***** Parent Thread *****/
int FDs[2];     /* create the place holder for the new pipe */
pipe(FDs); /* create the pipe: FDs[0]=input, FDs[1]=output */
char buffer[1024];

/*---Create the thread using pthread_create() ---*/
write(FDs[1], buffer, buffer_len); /* Send message to child */
...
/*---(Leave pipe closure to child)---*/
pthread_join(pchild, arg);
```
```

The child process or thread fulfills different roles. While similar to each other and due to the constraints on threads, they work slightly differently with pipes. Compare Listing 7.10 with Listing 7.11.

# LISTING 7.10  Creating Pipes in a Child Process

```
```c
/***** Child Process *****/
int FDs[2];     /* create the place holder for the new pipe */
pipe(FDs); /* create the pipe: FDs[0]=input, FDs[1]=output */
char buffer[1024];

/*---Create the child process---*/
dup2(FDs[0], 0); /* replace stdin */
```
```