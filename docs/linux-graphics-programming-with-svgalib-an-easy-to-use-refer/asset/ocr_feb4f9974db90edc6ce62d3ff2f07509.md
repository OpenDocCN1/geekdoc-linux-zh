```
/* code using no goto or comefrom function */
#endif
```

If you're compiling with an SVGA*lib that supports this feature, try to rearrange your source to work without it if an SVGA*lib version prior to 1.2.11 is used. The function should be called right after `vga_init()`. The `bg_test` demo shows the principle operation.

Note that background capabilities are in *very early stages*. Do not expect that *everything* will work flawlessly when background capabilities are enabled in your programs. Here's an example:

```
vga_init();
vga_setmode(G32x200x256);
if (vga_runinbackground_version() — 1)
{
vga_runinbackground(1);
}
```

See the man page for additional information.

```
*int* `vga_runinbackground_version(void)`
```

This returns the version of the current background support. In case SVGA*lib is compiled without background support, 0 is returned. See `vga_runinbackground()` for more information on background support.

# ## Debugging Aids

These functions are basic debugging aids:

```
*int* `vga_dumpregs(void)`
```

This function dumps the current values of all VGA registers in a way that can by copied in a source file. This is for debugging purposes only.

```
*void* `vga_gettextfont(void *font);` *void* `vga_puttextfont(void *font)`
```

These functions give access to the buffer where SVGA*lib saves the font used by the kernel. This is used by the `restorefont()`, `savetextmode()`, and `textmode()` utilities to restore a possibly corrupted console font.

The font buffer occupies 8,192 bytes. However, versions 1.2.13 and later use a larger buffer internally, and the size of the buffers passed to `vga_gettextfont()` and `vga_puttextfont()` can be set with `vga_ext_set()`.

These two functions give access to the internal buffers of SVGA*lib, not the font tables of the VGA card. This means that both functions must be called upon entering a graphics mode, and a newly set font takes effect only at the next `vga_setmode(TEXT)` call.