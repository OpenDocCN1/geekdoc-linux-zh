number or a mode name. See `vga_setmode()` for a partial list of predefined return values and their meanings. The mode names that can be used in the environment are those used by `vga_getmodename()` and `vga_getmodenumber()`.

Whenever your application has no special need for a given mode, you should always try to honor this setting for consistency among SVGAlib applications.

```
```c
int vga_lastmodenumber(void)
```
```

Returns the last video mode number. Because video mode numbers start with 1 (0 is for text mode), this allows an application to scan through all possible modes portable with `vga_modeinfo()`. For an example, see the `vga_test` demo. Note that `<vga.h>` includes this line:

```
```c
#define GLASTMODE vga_lastmodenumber()
```
```

```
```c
char *vga_getmodename(int mode)
```
```

A pointer to a static memory buffer is returned. Depending on the current mode, it consists of a capital G, followed by the amount of x pixels, followed by a lowercase x, then the amount of y pixels, and then another lowercase x. Finally, the number of colors is appended.

Here, the shortcuts 32K, 64K, 16M, and 16M4 are used in lieu of 32,768, 65,536, and 16,777,216 colors, respectively. 16M4 also refers to 16,777,216 colors, which are stored in 4 bytes (the highest address byte is unused) for easier screen access.

For unsupported modes, an empty string (`""`) is returned. In general, the string resembles the corresponding `#define` for the video mode in `<vga.h>`. For example, `vga_getmodename(10)` returns G640x480x256.

```
```c
int vga_getmodenumber(char *name)
```
```

This function parses *name and tries to find a video mode corresponding to it. *name is parsed case insensitively and should be either an integer string just giving a mode number or consist of a capital G, followed by the amount of x pixels, followed by a lowercase x, followed by the amount of y pixels, followed by a lowercase x. Finally, the number of different colors is appended.

Here, the shortcuts 32K, 64K, 16M, and 16M4 are used in lieu of 32,768, 65,536, and 16,777,216 colors, respectively. 16M4 also refers to 16,777,216 colors, which are stored in 4 bytes (the highest address byte is unused) for easier screen access.

For unsupported values (or the string `"PROMPT"`), the value -1 is returned. In addition, an irritating error message is printed to `stdout`. This is used during parsing the `SVGAlib_DEFAULT_MODE` environment variable. It should probably not be used for anything else. For example, `vga_getmodenumber("G640x480x256")` returns 10.