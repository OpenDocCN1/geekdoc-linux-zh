# ## Controlling VC Switches

These next functions involve controlling the VC switches:

# **void vga_lockvc(void)**

Disables virtual console switching for safety. Recommended when performing register I/O or low-level device handling. Used by mouse functions. Also useful in conjunction with background running.

# **void vga_unlockvc(void)**

Reenables virtual console switching.

# **vga_oktowrite(void)**

Indicates whether or not the active program is running in the console currently visible on the screen. That is, it checks as to whether it's ok to write to video memory (if running in the background has been allowed with the function above). Note that this is never entirely safe, since a console switch interrupt may occur during a video operation. Therefore, it's best to avoid this function.

Usually your program will be suspended when it has no access to the screen, but see `vga_runinbackground()` for an alternative.

# **void vga_runinbackground(int stat)**

Enables/disables background running of a graphics program. If `stat = 1`, then background running is enabled; if `stat = 0`, it's disabled. Normally, the program is suspended while not in the current virtual console. A program can only safely run in the background if it doesn't have any video access during this time.

As of version 1.2.11, this was changed by Pekka T. Ala-riikka and Michael Friman so that support for this must be enabled in your Makefile.cfg (which it is by default). Several ways to support this function may exist internally. As of now, only one using proc-fs works. Using `vga_runinbackground(VGA_GOTOBACK, void (*goto)())` and `vga_runinbackground(VGA_COMEFROMBACK, void (*comefrom)())` with function pointers to functions `void goto(void)` and `void comefrom(void)`, you can set up this function to be called when your program goes to background mode and when it returns to the foreground. These can be changed at any time, and passing NULL as a function disables the feature.

Both these new features require a `vga_runinbackground_version()` of 1 or higher. You shouldn't call it when the SVGAlib in use returns 0. Also, when writing applications, you can check with this:

```
#define VGA_GOTOBACK
/* code using vga_runinbackground(VGA_GOTOBACK, goto) */
#else
```