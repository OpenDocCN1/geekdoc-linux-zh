# Bitmap File Header

The **BITMAPFILEHEADER** data structure contains information about the type, size, and layout of a *device-independent bitmap* (DIB) file:

```
```c
typedef struct tagBITMAPFILEHEADER {
    WORD    bfType;
    DWORD   bfSize;
    WORD    bfReserved1;
    WORD    bfReserved2;
    DWORD   bfOffBits;
} BITMAPFILEHEADER;
```
```

The **BITMAPFILEHEADER** data structure contains the fields shown in Table 9.1.

A **BITMAPINFO** data structure immediately follows the **BITMAPFILEHEADER** structure in the DIB file.

# Bitmap Info

The **BITMAPINFO** structure fully defines the dimensions and color information for a Windows 3.0 device-independent bitmap:

```
```c
typedef struct tagBITMAPINFO {
    BITMAPINFOHEADER    bmiHeader;
    RGBQUAD             bmiColors[];
} BITMAPINFO;
```
```

> **Note**
> *3.0 refers to the bitmap format, and not to a particular version of Windows.*

The **BITMAPINFO** structure contains the fields shown in Table 9.2.

A Windows 3.0 device-independent bitmap consists of two distinct parts: a **BITMAPINFO** data structure that describes the dimensions and colors of the bitmap, and an array of bytes that define the pixels of the bitmap. The bits in the array are packed together, but each

| Table 9.1 BITMAPFILEHEADER. | |
| --- | --- |
| Field | Description |
| bfType | Specifies the type of file. It must be BM. |
| bfSize | Specifies the size, in **DWords**, of the file. |
| bfReserved1 | This is reserved and must be set to zero. |
| bfReserved2 | This is reserved and must be set to zero. |
| bfOffBits | Specifies, in bytes, the offset from the bitmap file header of the actual bitmap in the file. |