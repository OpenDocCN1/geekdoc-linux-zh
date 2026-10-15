The child's code is the next branch, in which 0 == pid is true. The child increments the values of two variables, one, global, declared globally and one, local, locally in main(). It then prints out their values, jumps over the parent code and executes the printf(), obtaining its process-id using the getpid() system call and displaying the values of local and global again.

In the meanwhile, the parent sleeps for two seconds, enough time so that the child's output will appear first. It then executes the printf(), obtaining its process-id using the getpid() system call and displaying the values of local and global. The sleep() prevents intermingling of the output, which can happen because the child shares the terminal with the parent.

Bearing in mind that the child is given a copy of the memory image of the parent, what should the output of the parent be? Hopefully you said that local = 0 and global = 10. This is because the child changed their values in the copy of the memory image, not in a shared memory. The point of this program is simply to demonstrate this important fact.

Let us make sure we understand fork() arithmetic before continuing. Before running the program forkdemo2.c shown in Listing 7.3, predict the number of lines of output. Do not redirect the output or pipe it. This will be explained afterward.

# Listing 7.3: forkdemo2.c

```
#include <unistd.h>
#include <stdio.h>
#include <stdlib.h>

int main( int argc, char* argv[] )
{
    int i;
    printf("About to create many processes...\n");
    for ( i = 0; i < N; i++ )
        if ( -1 == fork() )
            exit(1);

    printf("Process id = %d\n", getpid());
    fflush(stdout);    /* force output before shell prompt */
    sleep(1);          /* give time to the shell to display prompt */
    return 0;
}
```

Did you correctly predict?

Each time the bottom of the loop is reached, the number of processes in existence is twice what it was before the loop was entered, because each existing process executes the fork() call, making a copy of itself. If N were 1, the loop would execute once and there would be 2 processes, each printing their process ids to the screen. If N were 2, the loop would execute a second time, and the 2 processes would make 2 more, 4 in total. In general, there will be 2^N processes when the loop finishes, and that many lines of output on the screen, together with the first line,

About to create many processes...

for a total, when N = 4, of 17 lines. Now try redirecting the output of the program to wc, to make it easier to count how many lines are there.