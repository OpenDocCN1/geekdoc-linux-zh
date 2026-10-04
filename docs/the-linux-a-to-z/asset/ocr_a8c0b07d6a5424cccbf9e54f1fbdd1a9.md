its execution, as you have seen.

This suggests that in order to switch contexts between two threads within a single process, all that is required is to swap the values in a few processor registers – specifically, the program counter (or instruction register), ebp and the current stack pointer. In fact, you will soon see that all that really needs to be saved is the current ebp value, and that the other values can be derived from this.

Each thread has associated with it a data structure, which is used to save the per thread context when the thread is not currently running. The data structure has the following layout:

```
struct context
{
    int ebp;
    char *stack;
    struct context *next;
    struct context *prev;
};
```

The next and prev fields of the structure are used to form the forward and backward links that tie this structure into the doubly linked, circular list of structures which form the scheduling loop. The stack field is a pointer to an array of bytes which is used as the private stack space for this thread, and the ebp field is used as a temporary store for the contents of the processor ebp register when the CPU is processing some other thread.

# 29.4 Context Switching

The first piece of threads library code to look at is the release() function, which is called by a thread when it wants to pass its control of the CPU on to the next thread in the scheduling loop. When you examine this code, keep in mind that the variable current is a pointer to the struct context associated with the currently running thread:

```
release(void)
{
    /* 1 */
    if (thread_count<=1)
        return 0;

    /* 2 */
    current = current->next;
    switch_context(current->prev, current);
    return 1;
}
```