+   SIGTERM (15) - Offer the program to shut down (this signal, unlike SIGKILL, may be ignored)

The default action for all of these signals, except for SIGSEGV, is to terminate the program (an additional memory dump ( core dump ) is generated for SIGSEGV - a file that stores the image of the process address space for later analysis).

# ## Setting The Signal Layout

A sigaction () system call is used to set the signal disposition.

```
#include <signal.h>
int sigaction (int signum, // signal number
            struct sigaction * action, // new layout
            struct sigaction  * old_action); // return the previous disposition
```

The exposition is described using the sigaction structure with the following fields:

+   - sa_handler - pointer to the signal processor function
+   - sa_mask - the signal mask that specifies which signals will be blocked inside the processor
+   - sa_flag - additional checkboxes

Limit to zeroing sa_mask and sa_flag (without blocking any signal):

```
struct sigaction action = {0};
```

The sa_handler field should be set as a pointer to a previously declared function that looks like this:

```
void user_handler (int signum)
{
    // signal processing
```