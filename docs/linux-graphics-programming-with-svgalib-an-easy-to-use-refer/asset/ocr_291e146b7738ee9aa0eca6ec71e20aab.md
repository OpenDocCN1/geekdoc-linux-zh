**Table 9.4 Fields in BITMAPINFOHEADER.**

| Field | Description |
|---|---|
| biSize | Specifies the number of bytes required by the BITMAPINFOHEADER structure. |
| biWidth | Specifies the width of the bitmap in pixels. |
| biHeight | Specifies the height of the bitmap in pixels. |
| biPlanes | Specifies the number of planes for the target device and must be set to 1. |
| biBitCount | Specifies the number of bits per pixel. This value must be 1, 4, 8, or 24. |
| biCompression | Specifies the type of compression for a compressed bitmap. It can be one of the following values: | | • BI_RGB—Specifies that the bitmap is not compressed. | | • BI_RLE8—Specifies a run-length encoded format for bitmaps with eight bits per pixel. The compression format is a 2-byte format consisting of a count byte followed by a byte containing a 2-byte format consisting of a count byte followed by a byte containing a 2-byte format consisting of a count byte followed by a byte containing a color index. See the following section for more information. | | • BI_RLE4—Specifies a run-length encoded format for bitmaps with four bits per pixel. The compression format is a 2-byte format consisting of a count byte followed by two word-length color indexes. See the following section for more information. |
| biSizeImage | Specifies the size, in bytes, of the image. |
| biXPelsPerMeter | Specifies the horizontal resolution, in pixels per meter, of the target device for the bitmap. An application can use this value to select a bitmap from a resource group that best matches the characteristics of the current device. |
| biYPelsPerMeter | Specifies the vertical resolution, in pixels per meter, of the target device for the bitmap. |
| biClrUsed | Specifies the number of color indexes in the color table actually used by the bitmap. If this value is 0, the bitmap uses the maximum number of colors corresponding to the value of the biBitCount field. See the description of the BITMAPINFO data structure, earlier in this chapter, for more information on the maximum sizes of the color table. If biClrUsed is nonzero, the biClrUsed field specifies the actual number of colors that the graphics engine or device driver will access if the biBitCount field is less than 24. If the biBitCount field is set to 24, the biClrUsed field specifies the size of the reference color table used to optimize performance of Windows color palettes. If the bitmap is a “packed” bitmap (that is, a bitmap in which the bitmap array immediately follows the BITMAPINFO header and is referenced by a single pointer), the biClrUsed field must be set to 0 or to the actual size of the color table. |
| biClrImportant | Specifies the number of color indexes that are considered important for displaying the bitmap. If this value is 0, all colors are important. |

When the biCompression field is set to BI_RLE8, the bitmap is compressed using a run-length encoding format for an 8-bit bitmap. This format may be compressed in either of two modes:

+   - 7—Encoded
+   - 7—Absolute

Both modes can occur anywhere throughout a single bitmap.