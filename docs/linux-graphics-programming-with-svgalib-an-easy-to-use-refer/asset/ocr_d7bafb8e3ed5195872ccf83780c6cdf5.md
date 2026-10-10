Table 9.2 BITMAPINFO.
| Field | Description |
| :--- | :--- |
| **bmiHeader** | Specifies a BITMAPINFOHEADER data structure that contains information about the dimensions and color. |
| **bmiColors** | Specifies an array of RGBQUAD data structures that define the colors in the bitmap. |

scanline must be zero-padded to end on a LONG boundary. Segment boundaries can appear anywhere in the bitmap, however. The origin of the bitmap is the lower-left corner.

The **biBitCount** field of the BITMAPINFOHEADER structure determines the number of bits that define each pixel, as well as the maximum number of colors in the bitmap. This field may be set to any of the values shown in Table 9.3.

The **biClrUsed** field of the BITMAPINFOHEADER structure specifies the number of color indexes in the color table actually used by the bitmap. If the **biClrUsed** field is set to 0, the bitmap uses the maximum number of colors corresponding to the value of the **biBitCount** field.

The colors in the **bmiColors** table should appear in order of importance. Alternatively, for functions that use device-independent bitmaps, the **bmiColors** field can be an array of 16-bit unsigned integers that specify an index into the currently realized logical palette instead of explicit RGB values. In this case, an application using the bitmap must call device-independent bitmap functions with the *wUsage* parameter set to *DIB\_PAL\_COLORS*.

Table 9.3 BITMAPINFOHEADER.
| Value | Meaning |
| :--- | :--- |
| 1 | The bitmap is monochrome, and the **bmiColors** field must contain two entries. Each bit in the bitmap array represents a pixel. If the bit is clear, the pixel is displayed with the color of the first entry in the **bmiColors** table; if the bit is set, the pixel has the color of the second entry in the table. |
| 4 | The bitmap has a maximum of 16 colors, and the **bmiColors** field contains up to 16 entries. Each pixel in the bitmap is represented by a 4-bit index into the color table. For example, if the first byte in the bitmap is 0x1f, the byte represents two pixels. The first pixel contains the color in the second table entry, and the second pixel contains the color in the 16th table entry. |
| 8 | The bitmap has a maximum of 256 colors, and the **bmiColors** field contains up to 256 entries. In this case, each byte in the array represents a single pixel. |
| 24 | The bitmap has a maximum of 2$^{24}$ colors. The **bmiColors** field is **NULL**, and each three bytes in the bitmap array represents the relative intensities of red, green, and blue, respectively, of a pixel. |