# Linux Kernel 0.01

# Did You Know...

```
console.c

/*
 * This module implements the console I/O functions
 * Linux console driver
 *
 * Hopefully this will be a rather complete VT102 implementation.
 */

/* NOTE: We sometimes disable and enable interrupts for a short while
 * to put a word in video RAM, but this will work even for keyboard
 * interrupts. We know interrupts aren't enabled when getting a keyboard
 * interrupt, as we use trap-gates. Hopefully all is well.
 */

#include <linux/sched.h>
#include <linux/tty.h>
#include <asm/io.h>
#include <asm/system.h>

#define SCREEN_START 0xb8000
#define SCREEN_END   0xbffff
#define LINES 25
#define COLUMNS 80
#define SPAR 16

extern void keyboard_interrupt(void);

static unsigned long origin=SCREEN_START;
static unsigned long scr_end=SCREEN_START+LINES*COLUMNS*2;
static unsigned long pos;
static unsigned long top;
static unsigned long bottom=LINES;
static unsigned long lines=LINES*COLUMNS;
static unsigned long state;
static unsigned long spar_pos=SPAR;
static unsigned long spar_char;
static unsigned long spar_attr=0x07;
```

DID YOU KNOW... that the first Linux kernel, as programmed by Linus Torvalds, only occupied 65KB of memory? And that since version 0.01, the Linux kernel now boasts over 18 million lines of code. Not bad for a university project that now runs the New York Stock Exchange, and powers the US Department of Defence’s fleet of nuclear submarines.