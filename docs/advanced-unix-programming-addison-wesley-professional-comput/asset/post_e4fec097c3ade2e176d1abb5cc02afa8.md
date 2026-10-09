
EC_CLEANUP_BGN
  @exit(EXIT_FAILURE);
EC_CLEANUP_END
}

static void dummy_handler(int signum, siginfo_t *info, void *context)
{
}

Note that four signals are generated before the thread is even created, to demonstrate that they will be queued. It’s guaranteed that the `MYSIG_COUNT` signals will be accepted before `MYSIG_STOP` because they have a lower number. Also note that the signals are blocked and stay blocked. The dummy handler is needed because we must set `SA_SIGINFO` to turn on queuing. It so happens that Solaris queues the `RTS` signals no matter what, but you can’t count on that in a portable program.

Here’s the output, proving that the signals were queued:

Got MYSIG_COUNT: value: One
Got MYSIG_COUNT: value: Two
Got MYSIG_COUNT: value: Three
Got MYSIG_STOP: terminating thread

If you only want to wait for a limited time, you can use `sigtimedwait`, which adds a time-out argument to `sigwaitinfo`:

![](img/41b4c8f6d6a5c349eee321a301703d97_660_0.png)

`sigtimedwait` waits for at most the number of nanoseconds specified by `ts` for a signal in `set` to become pending and be returned. If the time period expires, it returns −1 with `errno` set to `EAGAIN`. You can’t have a timeout of `NULL`. If both `timespec` members are zero and no signal in `set` is pending, `sigtimedwait` returns immediately, but this is not really a special case—it has timed-out.

### 9.5.6 sigevent Structure and SIGEV_THREAD

The RTS-generation functions other than sigqueue are described elsewhere, as listed in Section 9.5.1, but they all use a sigevent structure to specify what signal and value to send. I'll explain just the sigevent structure here.

![](img/41b4c8f6d6a5c349eee321a301703d97_661_0.png)

The signal to be sent (SIGRTMIN, say) goes into sigev_signo, and the value to go along with it goes into sigev_value. As with the other RTS features, it's guaranteed to work only for RTS signals. The sigev_notify member specifies how the signal is to be sent:

- **SIGEV_SIGNAL** Generate a signal, as though sigqueue had been called
- **SIGEV_THREAD** Start a thread, as though pthread_create had been called
- **SIGEV_NONE** Don't provide any notification, which usually doesn't make much sense

SIGEV_THREAD is the most interesting. It causes a new thread to be started when the event occurs, every time it occurs, and the function pointed to by sigev_notify_function becomes the start function for the thread. Normally, start functions have a pointer-to-void argument; in this case it's a pointer-to-union-sigval, which is more or less the same, since one of the union members is a void pointer. You can set the attributes for the thread with the sigev_notify_attributes member, but you can't make the thread joinable. If the member is NULL, the thread is detached by default, which is the opposite of what pthread_create does.

There's a lot of overhead in creating a thread, so clearly you don't want to specify SIGEV_THREAD unless the event is fairly rare and/or its generation represents a large amount of work relative to the cost of starting a new thread. For example, starting a new thread every time input arrives is probably overdoing it.

In case you're confused, creating a thread when a signal would otherwise be generated is completely different from having a thread waiting in `sigwait` (Section 9.2.2). All they have in common is that they both use threads.

## 9.6 Global Jumps

Normally, a function returns to its caller only by executing a return statement or, if it's a `void` function, by flowing off the end of its outer block, which is the same thing. But it's possible to jump to an arbitrary, but preplanned, point in the program with the Standard C functions `setjmp` and `longjmp`:

**setjmp**—set jump point

```c
#include <setjmp.h>
int setjmp(
    jmp_buf loc_info      /* saved location information */
);
/* Returns 0 if called directly, non-zero if from longjmp
   (no error return) */
```

**longjmp**—jump to jump point

```c
#include <setjmp.h>
void longjmp(
    jmp_buf loc_info,     /* saved location information */
    int val               /* value for setjmp to return */
);
```

You mark the location you want to jump to—the label, so to speak—with a call to `setjmp` that saves whatever location information it needs (e.g., current stack pointer, machine address) in its argument, which doesn't look like a pointer that can receive information, but is. Then, from within any function, no matter how deeply nested, you execute `longjmp` with that same argument and the effect is as if `setjmp` had returned `val`, which can't be zero; if it is, `setjmp` returns 1.

As calling the functions in which `longjmp` appears may have pushed data onto the stack, `longjmp` automatically pops it all off. The function containing the `setjmp` is not "called" and there is no recursion upon the return, although there may have been on the way to calling `longjmp`.

Here's an example. If you've never seen `setjmp` and `longjmp` before, you'll think it's pretty weird:

```c
static jmp_buf loc_info;

static void fcn2(void)
{
    printf("In fcn2\n");
    longjmp(loc_info, 1234);
    printf("Leaving fcn2\n");
}

static void fcn1(void)
{
    printf("In fcn1\n");
    fcn2();
    printf("Leaving fcn1\n");
}

int main(void)
{
    int rtn;

    rtn = setjmp(loc_info);
    printf("setjmp returned %d\n", rtn);
    if (rtn == 0)
        fcn1();
    printf("Exiting\n");
    exit(EXIT_SUCCESS);
}
```

And here’s the output:

```
setjmp returned 0
In fcn1
In fcn2
setjmp returned 1234
Exiting
```

So you can see that setjmp was called once but returned twice and that the jump went straight from the middle of fcn2 back to the middle of main; the two “leaving” lines weren’t printed.

If you don’t completely understand, don’t worry about it because I’m now going to say this: Don’t ever use longjmp. Here’s why:

- While the stack is cleaned up, little else (e.g., allocated memory, open files) is.
- There are some restrictions about where you can use setjmp and longjmp that will get you into trouble if you forget them.
- Some people (including me) don’t even like `goto` _within_ a function. They like `longjmp` much less. It makes programs very difficult to understand and maintain.
- The main use for `longjmp` is from within a signal handler, but it’s not async-signal-safe, so you can’t use it there unless you can guarantee that the signal handler was invoked by an async-signal-safe function, such as a `kill` executed from within the same process (Section 9.1.7).

If you think you need `longjmp`, it’s probably because you haven’t designed your functions well enough to allow them to return to their caller, perhaps with an indication of an error or other exceptional condition. Work harder and you’ll come up with something.

`longjmp` may or may not restore the signal mask. If you want to force it to be restored, there are variants of `setjmp`/`longjmp` that are identical, except that they can save and restore the signal mask:

**sigsetjmp**—set jump point

```c
#include <setjmp.h>
int sigsetjmp(
    sigjmp_buf loc_info,    /* saved location information */
    int savemask             /* non-zero to save signal mask */
);
/* Returns 0 if called directly, non-zero if from siglongjmp (no error return) */
```

**siglongjmp**—jump to jump point, restore signal mask if saved

```c
#include <setjmp.h>
void siglongjmp(
    sigjmp_buf loc_info,    /* saved location information */
    int val                  /* value for sigsetjmp to return */
);
```

The signal mask that gets restored is the one that was in effect when `sigsetjmp` was called. If `siglongjmp` is called from within a signal handler, which is what it was designed for, this may be different from what the signal handler would restore were it allowed to return normally.

Since `siglongjmp` is no more async-signal-safe than is `longjmp`, it can’t usually be used in a signal handler, and its added ability to restore the signal mask is therefore almost useless.
