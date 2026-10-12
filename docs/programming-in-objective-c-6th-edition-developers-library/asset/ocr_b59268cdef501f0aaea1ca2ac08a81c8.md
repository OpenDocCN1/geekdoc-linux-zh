```
```text
#define DEBON
# define DEBUG(level, fmt, ...) \ 
        if (Debug >= level) \ 
            fprintf (stderr, fmt, __VA_ARGS__)
#else
# define DEBUG(level, fmt, ...)
#endif
```
```