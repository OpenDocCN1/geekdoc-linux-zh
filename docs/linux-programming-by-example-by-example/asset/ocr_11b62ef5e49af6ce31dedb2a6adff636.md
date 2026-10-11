that set alarms also catch them, rather than allowing them to terminate the process.

# Using the pause Function

The `pause` function suspends the calling process until *any* signal arrives. The caller must be equipped to handle the delivered signal, or the signal's default disposition will occur. `pause` is also prototyped in `<unistd.h>`:

```
int pause(void);
```

`pause` returns to the calling process only if the process catches a signal. If the delivered signal invokes a handler, it will execute before `pause` returns. `pause` always returns -1 and sets `errno` to `EINTR`.

# Example

![](bbox=[0.04, 0.315, 0.125, 0.365])

# Example

This simple program just waits for a signal to be delivered, and then exits.

```
```
/*
**pause.c - Pause then exit
*/
#include <unistd.h>
#include <stdlib.h>

int main(void)
{	pause();
	exit(EXIT_SUCCESS);
}
```
```

![](bbox=[0.04, 0.635, 0.125, 0.68])

# Output

```
```
$ ./pause
[Ctrl+z]

[1]+  Stopped              ./pause
fg
./pause
[Ctrl+\]
Quit (core dumped)
$ ./pause
User defined signal 1
```
```

In the first run, `pause` just goes into an eternal holding pattern. First, `Ctrl+Z` (entered from the keyboard), suspends the program; the `fg` command brings it to the foreground again, at which point `Ctrl+\` (`SIGQUIT`) terminates it.