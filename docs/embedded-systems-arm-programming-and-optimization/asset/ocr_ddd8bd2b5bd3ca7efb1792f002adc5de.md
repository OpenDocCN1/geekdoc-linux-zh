# 114 CHAPTER 3 Arithmetic Optimization and the Linux Framebuffer

myFile = fopen("lena.ppm","r");  (open the file, assume hardcoded name)

if (!myFile) (perror("image file");exit(0)); (check for error)

fscanf(myFile,"%d",&cols); (try to read column number)

while (cols<160) { (search file for legitimate "cols" value)

fseek(myFile,1,SEEK_CUR); (advance file pointer one character)

fscanf(myFile,"%d",&cols); (try again)

}

fscanf(myFile,"%d",&rows); (try to read row number)

while (rows<120) { (search file for legitimate "rows" value)

fseek(myFile,1,SEEK_CUR); (advance file pointer one character)

fscanf(myFile,"%d",&rows); (try again)

}

fscanf(myFile,"%d",&maxcolorvalue); (try to read row number)

while (!maxcolorvalue) { (search leg. "maxcolorval")

fseek(myFile,1,SEEK_CUR); (advance file pointer one character)

fscanf(myFile,"%d",&maxcolorvalue); (try again)

}

In a PPM file, each pixel is stored as three bytes representing RGB intensity.
Use this 24-bit format to store the image in memory.

Now that the program has the row and column count it can allocate
rows × columns × 3 bytes. src_image is declared as an unsigned character
pointer (unsigned char *).

```
src_image=(unsigned char*)malloc(rows*cols*3); (allocate mem-
ory for image)
```

```
if (!src_image) { (check return value of malloc)
```

```
perror("Allocating memory for source image"); (allocate;
exit(0);
```

```
}
```