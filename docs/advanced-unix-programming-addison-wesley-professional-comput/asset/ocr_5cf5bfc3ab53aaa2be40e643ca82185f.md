cess finishes with the resource, it unlinks the file. One of the unsuccessful processes’ opens will then work, and it can safely proceed.

For this to work, the checking to see if the file exists (with `access`, say, which is in Section 3.8.1) and the creating of it have to be atomic (indivisible)—no other process can be allowed to execute in the interim, or it might create that very file *after* the first process has already checked. So don’t do this:

```
if (access(…) == 0)     /* file does not exist */
  … open(…) …          /* create it */
```

We need a more reliable method that guarantees atomicity.

A simple exclusivity mechanism like this is called a *mutex* (short for mutual exclusion), a *binary semaphore* (can count only up to 1), or a *lock*. We’ll hit these things several times throughout this book; see Section 1.1.7 for a quick rundown. In the UNIX world, the word “mutex” is more often used in the context of threads and the word “semaphore” suggests something that uses the UNIX semaphore system calls, so we’ll just call it a “lock” in this section.

The protocol is best encapsulated into two functions, *lock* and *unlock*, to be used like this:

```
if (lock("accounts")) {
  … manipulate accounts …
  unlock("accounts");
}
else
  … couldn’t obtain lock …
```

The lock name “accounts” is abstract; it doesn’t necessarily have anything to do with an actual file. If two or more processes are concurrently executing this code, the lock will prevent them from simultaneously executing the protected section (“manipulate accounts,” whatever that means). Remember that if a process doesn’t call *lock*, though, then there is no protection. They’re *advisory* locks, not *mandatory*; (See Section 7.11.5 for more on the distinction between the two.)

Here is the code for *lock*, *unlock*, and a little function *lockpath*:

```
#define LOCKDIR "*/tmp/*"
#define MAXTRIES 10
#define MAPLENGTH 2

static char *lockpath(char *name)
{
    static char path[100];
```