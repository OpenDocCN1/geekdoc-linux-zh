finished rotated image as a pointer to the calling main program.

This covers the algorithm for rotating a photo in memory by 180 degrees. But how does the image, which is compressed in JPEG format on disk, find its way into RAM as a pixel matrix in the first place? The imgtool() function in Listing 3 takes the name of the photo file in srcFile, the name of the target file as the second parameter, and, as the third parameter, a callback function that performs the desired rotation of the image in RAM. Functions are full-featured data types in Go and can easily be passed to other functions, which basically tells Go: "Here's the algorithm to apply to the original image data." Listing 3 opens the original file for reading in line 11, uses Decode() to decode the JPEG data with the standard image/jpeg package, and stores the results into a matrix pointed to by the jimg variable if there are no errors. Line 21 then calls the function previously passed in as a parameter with the variable cb, passes the image data in jimg to it, and receives the modified data of the then rotated image in dimg. All that remains is to create a new destination file, dstFile, and write the JPEG-encoded data for the modified photo in line 30.

clockwise to display it with the correct orientation. In Figure 4, Gimp determines that a photo of the little-known Billy Goat Hill park in San Francisco needs to be rotated a quarter turn to the right and offers to complete the task right away.

But how does a quarter rotation of the pixels work in a 2D matrix? Figure 5 shows schematically how the first row of pixels with the values (1,2,3,4) ends up as the rightmost column in the result after rotating the matrix clockwise by 90 degrees.

While the algorithm converts rows into columns, the target image's dimension also changes. Cell phone photos are typically rectangular rather than square, and a photo rotated 90 degrees not only changes its pixel values but also swaps the width and height of the resulting overall image. Listing 4 accounts for this by having line 10 swap the dimensions in bounds in the X and Y direction, so that the modifiable target image generated in line 12 by NewRGBA() already has the dimensions of the rotated rectangle rather than those of the original.

# ## Rotating 90 Degrees

Not all incorrectly saved images are upside down. Sometimes the images are also on their sides and need to be rotated by 90 degrees. In these cases, calling exiftool will display something like Orientation: 90 CW for the JPEG file. This indicates that you need to rotate the image 90 degrees

# ## Changing X to Y

The double for loop starting in line 14 of Listing 4 iterates line by line through the source image, retrieves the current

```
Listing 3: imgmod.go

```go
01  package main
02
03  import (
04      "image"
05      "image/jpeg"
06      "log"
07      "os"
08  )
09
10  func imgMod(srcFile string, dstFile string, cb func(image.Image) *image.RGBA) {
11      f, err := os.Open(srcFile)
12      if err != nil {
13          log.Fatalf("os.Open failed: %v", err)
14      }
15
16      jimg, _, err := image.Decode(f)
17      if err != nil {
18          log.Fatalf("image.Decode failed: %v", err)
19      }
20
21      dimg := cb(jimg)
22      if err != nil {
23          log.Fatalf("Modifier failed")
24      }
25
26      f, err = os.Create(dstFile)
27      if err != nil {
28          log.Fatalf("os.Create failed: %v", err)
29      }
30
31      err = jpeg.Encode(f, dimg, nil)
32      if err != nil {
33          log.Fatalf("jpeg.Encode failed: %v", err)
34      }
35  }
```
```

![](bbox=[0.51, 0.55, 0.94, 0.88])

Figure 4: Gimp notices that the image needs to be rotated by 90 degrees.