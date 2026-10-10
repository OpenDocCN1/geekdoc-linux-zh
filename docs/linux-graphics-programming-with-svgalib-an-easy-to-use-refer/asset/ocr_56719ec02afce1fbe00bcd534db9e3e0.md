ses" fade. Given that fact, you might be tempted to hard-code a delay, using something along the lines of this:

```
for (k = 0; k < 100000; k++) { }
```

But wait! That might look good on your machine, but how might it look on someone else’s computer, which may well have a faster (or slower) processor? As processors continue to improve, your code will almost assuredly become obsolete. Doing it that way would be shooting yourself in the foot. Instead, it's time to delve into the black art of subsecond delays.

# Subsecond Delays

Actually, it’s not that big of a deal. I prefer to use usleep(unsigned long usec), which lets me pause in microsecond intervals (millionths of a second), but there’s also nanosleep(const struct timespec *req, struct timespec *rem), which allows pauses in the billionths of a second. The point I wanted to make previously was merely that you shouldn’t rely on empty loops for delays.

USleep() is defined in <unistd.h>, whereas nanosleep() is in <time.h>. You might prefer to investigate nanosleep(), because according to the man page, it “has the advantage of not affecting any signals, it is standardized by POSIX, it provides higher timing resolution, and it allows [you] to continue a sleep that has been interrupted by a signal more easily.” Well said. As for me, I prefer the simplicity of usleep().

# Screen Fades With Vgafl

Listing 6.3 demonstrates the same cinematic fade routine shown in Listing 6.2, but modified to use vgafl and usleep(). Because vga_getcolors() is no longer useful, you can use the COLORS constant defined in <vgafl.h> to get the same value. Here’s the syntax:

```
#define COLORS (currentcontext.colors)
```

I also shortened the range of shades some; you may have noticed that the screen became sufficiently dark before the RGB values hit true black (0, 0, 0), so it’s pointless to spiral down through every last value. Again, the 0-to-63 shade scale is the default, unless you employ vga_ext_set().

# Listing 6.3 A more realistic fade.

```
int i,
  j,
  r,
  g,
  b;

for (i = 64; i > 5; i--)
```