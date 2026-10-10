# **STRIDE**

| N1,N2,N3 | INC2Y | INC3Y |
| :--- | :--- | :--- |
| | 30 | 32 | 976 |
| | 32 | 34 | 1104 |
| | 64 | 66 | 4256 |
| | 120 | 122 | 14640 |
| | 128 | 130 | 16656 |
| | 240 | 242 | 58128 |
| | 256 | 258 | 66064 |
| | 420 | 422 | 177240 |

For this subroutine, the *strides* ($inc2x$ and $inc3x$) of the input array are also important. In general, $inc2x = inc2y/2$ and $inc3x = inc3y/2$ are good choices. These are also the requirement if you want to use the same array for input and output.