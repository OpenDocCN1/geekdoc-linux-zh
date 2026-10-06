
## 3.4 Floating-Point Image Transformation

![](img/e6ebc663bbb86c6e7bf9ef22ad136e6f_115_0.png)

- FIGURE 3.1 Fractional source pixel.

intermediate calculations. Typecasting between integers and floating point requires the use of high latency conversion instructions.

In order to characterize the overhead added by these operations, begin by implementing the image transformation using floating point and measuring its performance using the performance counters.

Our objective is to generate a video consisting of a sequence of frames depicting the image smoothly rotating around all three axes. Graphically, this will appear as a 2D image rotating in 3D space.

To do this, gradually change the X, Y, and Z rotation of the image in each frame. For this program, you need to call a function before each frame that computes the transformation matrix for a given X, Y, and Z rotation angles. Since this function is called once per frame (as opposed to once per pixel), it is reasonable to expect it to have a negligible effect on performance.

The following function will calculate the transformation matrix as a function of X, Y, and Z angles and returns the first two rows and first columns of the transformation matrix as arrays c_row and c_col:

```c
void calc_coeffs(float c_row[2], float c_col[2], float scale, float rot_x, float rot_y, float rot_z) {
    int i, j, k;
    float rotm_x[3][3] = {{1.0, 0.0, 0},
                          (0, 1.0/cos(rot_x), tan(rot_x)},
                          (0, tan(rot_x), -1.0/cos(rot_x))};
    float rotm_y[3][3] = {{1.0/cos(rot_y), 0, -tan(rot_y)},
                          (0, 1.0, 0),
                          (tan(rot_y), 0, 1.0/cos(rot_y))};
    float rotm_z[3][3] = {{cos(rot_z), -sin(rot_z), 0},
                          (sin(rot_z), cos(rot_z), 0},
                          {0, 0, 1.0}};
    float tempm0[3][3], tempm1[3][3], tempm2[3][3], sum;

    for (i=0; i<3; i++) // (temp = Ax * Ay)
        for (j=0; j<3; j++) {
            sum=0.0;
            for (k=0; k<3; k++) sum+=rotm_x[i][k]*rotm_y[k][j];
            tempm0[i][j] = sum;
        }
    for (i=0; i<3; i++) // (temp = temp * Az)
        for (j=0; j<3; j++) {
            sum=0.0;
            for (k=0; k<3; k++) sum+=tempm0[i][k]*rotm_z[k][j];
            tempm1[i][j] = sum;
        }
    c_row[0] = tempm1[0][0];
    c_row[1] = tempm1[0][1];
    c_col[0] = tempm1[1][0];
    c_col[1] = tempm1[1][1];
}
```

### 3.4.1 Loading the image

Begin by loading a source image into memory. Find a suitable image online, as the color version of the famous 512 pixel by 512 pixel “Lena” image commonly used for image processing work. First you will need to convert the image to PPM format using an image editing tool on your workstation.

The PPM file format is an uncompressed or “raw” format, which is trivial to read and write in a program without needing any special image libraries.

A PPM file contains both ASCII text and binary data. A header appears at the beginning of the file that is comprised of ASCII text. The header is followed by binary data representing each row of the image in ascending row order (top to bottom). Each row is comprised of pixels ordered in ascending column order (left to right). Each pixel usually stored as three consecutive bytes corresponding to the red, green, and blue (RGB) color channels.

The PPM header consists of the following values in ASCII separated by whitespace (spaces, tabs, newlines, line feeds):

1. the format’s “magic number” P6,
2. the number of columns,
3. the number of rows, and
4. the maximum color value (usually 255).

PPM files may also contain comment lines that begin with #.

To read a PPM file and convert it into a 16-bit format in memory, begin with the following declarations:

```c
FILE *myFile; (file pointer)
int rows=0, cols=0, maxcolorvalue=0; (header information)
int i,j; (loop vars)
static unsigned short *src_image; (pointer to image in memory)
```

Next, open the file and read the header. The tool that converted the image to a PPM file may have inserted one or more lines of comments before the header. To skip these, repeatedly use the fscanf() function to search for integers, looking for the first integer that is large enough to represent each value in the header:

```c
myFile = fopen("lena.ppm","r");  (open the file, assume hardcoded name)

if (!myFile) {
    perror("image file");
    exit(0); (check for error)
}

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
while (!maxcolorvalue) { (search file for "maxcolorval")
    fseek(myFile,1,SEEK_CUR); (advance file pointer one character)
    fscanf(myFile,"%d",&maxcolorvalue); (try again)
}
```

In a PPM file, each pixel is stored as three bytes representing RGB intensity.
Use this 24-bit format to store the image in memory.

Now that the program has the row and column count it can allocate rows × columns × 3 bytes. src_image is declared as an unsigned character pointer (unsigned char *).

```c
src_image=(unsigned char*)malloc(rows*cols*3); (allocate memory for image)

if (!src_image) {
    perror("Allocating memory for source image"); (allocate;
    exit(0);
}
```

Advance the file pointer by one byte to move beyond the newline character after the header. Then read the contents of the image directly into the image array.

```c
fseek(myFile,1,SEEK_CUR);   (advance file pointer by one)
read(src_Image,1,rows*cols*3,myFile);   (read image contents)
```

### 3.4.2 Rendering frames

Initialize the X, Y, and Z angles to 0. Inside of an infinite while-loop, increment each by 1, 0.5, and 0.25 degrees per frame, respectively (0.0175,0.0087, and 0.0044 rad) and calculate the corresponding transformation matrix.

```c
while (1) {
    rot_x += 0.0175; // 1 degree per frame
    rot_y += 0.0087; // 0.5 degree per frame
    rot_z += 0.0044; // 0.25 degree per frame
    calc_coeffs(c_row, c_col, scale, rot_x, rot_y, rot_z);
```
