# 4.13 Performance Results

```
t_size.x = t_size.y = dims[k];
if (t_size.x550) (// tried all tile sizes,
  // now filter without tiling

k=0;
t_size.x = 640;
t_size.y = 480;
} else k++:
  capture_frame(&buf);
  filter_16bit_cam(buffer, t_size, 480, 640, fbp);
```

# 4.13 PERFORMANCE RESULTS

Figure 4.18 shows the cache miss rate and CPI for the filter function on the Raspberry Pi. The filter function includes tile conversion code and buffer output code. Note that some tile sizes are unnecessarily large compared to the frame size of 640 × 480.

The worst cache miss rate occurs when there is no tiling, but the worst CPI occurs with tile size 288×288. CPI improves slightly when tiling is disconnected. This is likely due to lower instruction CPI that results from the reduction of executed branch instructions from needing fewer iterations of the tile loops.

![](bbox=[0.236, 0.635, 0.803, 0.856])

**FIGURE 4.18** Cache miss rate and CPI for 2D Sobel edge detection filter for a range of square sizes, from 8×8 pixels to 352×352 pixels, and without tiling. This performance includes the function that converts and buffers each frame and the function that writes the buffer. Cache miss rate roughly correlates with average CPI. The highest-performing tile was 8×8, which provided a speedup of 1.7 in miss rate compared to the nontiled version.