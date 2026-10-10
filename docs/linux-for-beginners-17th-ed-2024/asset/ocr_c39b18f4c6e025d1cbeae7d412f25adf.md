![](bbox=[0.89, 0.04, 0.94, 0.08])

# # Linux Kernel 0.01

```
```c
/*
 * Copyright Linus Torvalds
 * Based on WRITE-BAKED 838-MODE - Q-51.1
 * Hopefully (this will be a faster complete VTI.01 implementation.
 */

/*
 * 838: The 838-SIM-1324-41-BRIDGE-DRIVER
 */

#include <linux/mod.h>
#include <asm/io.h>
#include <asm/bio.h>
#include <asm/segm.h>

#define SCREEN_DATA 128000
#define SCREEN_END  (0xC600)
#define LINES 25
#define COLUMNS 80
#define SPAM 16

extern void keyboard_interrupt(void);

static unsigned long origin=SCREEN_DATA;
static unsigned long mtr_end=SCREEN_DATA+LINES*(COLUMNS+2);
static unsigned long p0m;
static unsigned long top_i=bottom_LINE;
static unsigned long line_i=LINES*COLUMNS;
static unsigned long state;
static unsigned long npar,nar*(NPAR);
static unsigned long gear;
static unsigned char attr=NOT;
```
```

that the first Linus kernel, as programmed by Linus Torvalds, only occupied 65KB of memory? And that since version 0.01, the Linux kernel now boasts over 18 million lines of code. Not bad for a university project that now runs the New York Stock Exchange, and powers the US Department of Defence's fleet of nuclear submarines.

# ## DID YOU KNOW...