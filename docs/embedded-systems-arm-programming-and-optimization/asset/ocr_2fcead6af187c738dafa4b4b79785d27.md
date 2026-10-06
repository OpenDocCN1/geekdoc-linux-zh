# 4.10 APPLYING THE 2D TILED FILTER

The next step is to write a loop that applies the filter to each tile. The loop will iterate for each tile so it can be structured as a two-level nested loop.

This function should accept the image size and tile size as arguments, so before the loop, initialize a "struct tile" variable (named mytile in the code below) that it contains these sizes.

The program can use OpenMP to distribute the outer loop's workload across the thread pool. This way, each thread will process a set of tile rows.

The last tile in each dimension may straddle the image boundary, so the loop bound must "round up" partial tiles. To do this, use a ternary expression that adds one to the image-tile size quantity when the corresponding modulo is nonzero.

```
#pragma omp parallel for firstprivate(mytile)
for (i=0;i<i(mytile.image_size.y%mytile.tile_size.y);
    mytile.image_size.y/mytile.tile_size.y+1)
    mytile.image_size.y / mytile.tile_size.y;
    i++;

mytile.tile_loc.y = i;
for (j=0;j<mytile.image_size.x%mytile.tile_size.x
    mytile.image_size.x/mytile.tile_size.x+1)
    mytile.image_size.x / mytile.tile_size.x);j
    ++);

mytile.tile_loc.x = j;
```

For each tile the program must compute its internal limits to prevent the filter loop from exceeding the image boundaries in either dimension for any tile whose right or bottom edge extends beyond the image boundary.

Next, the tile is extracted from the YUV frame. From this data, perform the 2D version of both the X and Y Sobel operator. After computing the X and Y partial derivatives for each pixel, calculate the resultant norm. Lastly convert the tile to 16-bit RGB and write it into the frame buffer.

```
find_limit(&mytile,&limit);
extract_tile(in_image,&mytile.frame,3,&limit);
```