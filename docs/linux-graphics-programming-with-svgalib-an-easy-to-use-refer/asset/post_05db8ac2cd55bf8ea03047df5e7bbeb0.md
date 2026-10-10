
## int vga_getcurrentmode(void)

Returns the current video mode. See vga_setmode() for a partial list of predefined return values and their meanings.

## int vga_hasmode(int mode)

This function returns a nonzero value if the given mode is supported and 0 otherwise. See vga_setmode() for a list of predefined mode values and their meanings. vga_modeinfo() can be used to find out details about the specific mode.

## vga_modeinfo *vga_getmodeinfo(int mode)

This function returns a pointer to a statically allocated mode information structure that's filled out with details for video mode mode.

vga.h> defines vga_modeinfo as this:

```c
typedef struct {
	int width;
	int height;
	int bytesperpixel;
	int colors;
	int linewidth;
	int maxlogicalwidth;
	int startaddressrange;
	int maxpixels;
	int haveblit;
	int flags;
	/* Extended fields, not always available: */
	int chipset;
	int memory;
	int linewidth_unit;
	char *linear_aperture;
	int aperture_size;
	void (*set_aperture_page) (int page);
	void *extensions;
} vga_modeinfo;
```

If the given mode is out of range, NULL is returned.

### Warning

Beware. Even when vga_getmodeinfo() returns details about a certain mode, you must check to see whether it is currently available. With vga_hasmode(), this may depend on memory size and other details.

The field’s meaning in detail includes the basic mode details:

- Width—Width of the mode in pixels.
- Height—Height of the mode in pixel lines.
- Bytesperpixel—Bytes per pixel. This is 1, 2, 3, or 4 (for 256, 32K, and 64K; 16M, and 16M4 modes, respectively) and 0 for planar VGA modes.
- Linewidth—Logical scanline width in bytes. This is the memory offset between two pixels above each other in two adjacent screen lines. It’s not valid to assume that linewidth equals width times bytesperpixel.
- Colors—The number of colors you can display simultaneously: 2, 16, 256, 32,768, 65,536, or 16,777,216. Generally, 16 and 256 mean that a color lookup table is used. Two means that only black and white are used and the others use some high/true color mode.

Possible modifications of the memory layout include the following:

- Maxlogicalwidth—The maximum logical scanline width (in bytes) that you can set for this mode with vga_setlogicalwidth() and still expect a perfect screen image.
- Startaddressrange—The mask of changeable bits of the start address (in pixels). All zero bits in startaddressrange must also be zero in a call to vga_setdisplaysart() when you want to avoid noisy video signals.

Memory size includes this:

- Maxpixels—Maximum number of pixels that will fit in a logical screen (depends on video memory).

Advanced capabilities include the following:

- Haveblit—Indicates whether the following **bitblit** functions are available. It’s a logical value or one of the following predefined values (which have only one bit set):
  - HAVE_BITBLIT—Has a vga_bitblit() old-style accelerator function
  - HAVE_FILLBLIT—Has a vga_fillblit() old-style accelerator function
  - HAVE_IMAGEBLIT—Has a vga_imageblit() old-style accelerator function
  - HAVE_HLINEBLIT—Has a vga_hlinelistblit() old-style accelerator function
  - HAVE_BLITWAIT—Has a vga_blitwait() old-style accelerator function
- Flags—Miscellaneous flags. It’s a logical value or one of the following predefined values (which have only one bit set):
  - HAVE_RWPAGE—vga_setreadpage() and vga_setwritpage() are available in this mode.
  - IS_INTERLACED—The mode is interlaced, which means it will tend to flicker. The user might be happier if the application chooses another mode.
  - IS_MODEX—Mode X-like memory layout (planar 256 colors VGA mode). See vga_setmode(x) for some explanations.
  - IS_DYNAMICMODE—Dynamically loaded mode. This mode was defined in *etc/vga/libvga.conf* by the user, who will probably prefer its usage. However, as a general rule, this should be of no interest to you.
  - CAPABLE_LINEAR—The mode can be set to linear addressing with `vga_setlineaddressing()`.
  - IS_LINEAR—Linear addressing is already enabled for this mode.
  - EXT_INFO_AVAILABLE—The extended fields in this information structure are set to sensible information. If `EXT_INFO_AVAILABLE` isn't set, you shouldn't access these fields, as you might have encountered an old version of SVGAlib, and the fields might not have been allocated at all.
  - RGB_MISORDERED—For 16M4 modes, it means that the 4 bytes per pixel actually mean 0BGR rather than BGRO, as per default. For 16M modes, it means that the 3 bytes actually mean RGB instead of BGR. The first is a general limitation of Mach32; the latter of Mach32 with a RAMDAC of type 4. The VGA drawing functions take this into account.
  - HAVE_EXT_SET—A `vga_ext_set()` is available and can be called.

Extended mode information—Use must check for `EXT_INFO_AVAILABLE` in your flags before trying to access these values:

- `chiptype`—The chipset that was detected/set. This specifies a subtype of the current `vga_getchipset()`: setting whose value depends on the chipset. It should only be used internally or for debugging.
- `memory`—Memory available on the SVGA card in Kb.
- `linewidth`—Use only multiples of this value for `set_logicalwidth()` or `set_displaystart()` to ensure graceful alignment of lines onto the VGA memory in this mode and for noiseless video signals.
- `linear_aperture`—A pointer to a `mmap()`'d secondary linear frame buffer (not related to the use of `vga_setlineaddressing()`). NULL if unavailable.
- `aperture_size`—The size of the secondary frame buffer in KB. This is 0 if unavailable.
- `set_aperture_page`—A function taking an int as a parameter to select a page in the framebuffer addressed by read/writes to this memory array (if `aperture_size` < `memory`).
- `extensions`—Pointers to additional, internal, chipset-specific information (contents of the EEPROM for Mach32 driver).

The vgatest demo displays most of this information for all supported modes.

## int vga_getdefaultmode(void)

Returns the default graphics mode number from the SVGALIB_DEFAULT_MODE environment variable. This is -1 if undefined. The environment variable can either be a mode number or a mode name. See `vga_setmode()` for a partial list of predefined return values and their meanings. The mode names that can be used in the environment are those used by `vga_getmodename()` and `vga_getmodenumber()`.

Whenever your application has no special need for a given mode, you should always try to honor this setting for consistency among SVGAlib applications.

## int vga_lastmodenumber(void)

Returns the last video mode number. Because video mode numbers start with 1 (0 is for text mode), this allows an application to scan through all possible modes portable with `vga_modeinfo()`. For an example, see the `vga_test` demo. Note that `<vga.h>` includes this line:

```c
#define GLASTMODE vga_lastmodenumber()
```

## char *vga_getmodename(int mode)

A pointer to a static memory buffer is returned. Depending on the current mode, it consists of a capital G, followed by the amount of x pixels, followed by a lowercase x, then the amount of y pixels, and then another lowercase x. Finally, the number of colors is appended.

Here, the shortcuts 32K, 64K, 16M, and 16M4 are used in lieu of 32,768, 65,536, and 16,777,216 colors, respectively. 16M4 also refers to 16,777,216 colors, which are stored in 4 bytes (the highest address byte is unused) for easier screen access.

For unsupported modes, an empty string (`""`) is returned. In general, the string resembles the corresponding `#define` for the video mode in `<vga.h>`. For example, `vga_getmodename(10)` returns G640x480x256.

## int vga_getmodenumber(char *name)

This function parses *name and tries to find a video mode corresponding to it. *name is parsed case insensitively and should be either an integer string just giving a mode number or consist of a capital G, followed by the amount of x pixels, followed by a lowercase x, followed by the amount of y pixels, followed by a lowercase x. Finally, the number of different colors is appended.

Here, the shortcuts 32K, 64K, 16M, and 16M4 are used in lieu of 32,768, 65,536, and 16,777,216 colors, respectively. 16M4 also refers to 16,777,216 colors, which are stored in 4 bytes (the highest address byte is unused) for easier screen access.

For unsupported values (or the string `"PROMPT"`), the value -1 is returned. In addition, an irritating error message is printed to `stdout`. This is used during parsing the `SVGAlib_DEFAULT_MODE` environment variable. It should probably not be used for anything else. For example, `vga_getmodenumber("G640x480x256")` returns 10.
