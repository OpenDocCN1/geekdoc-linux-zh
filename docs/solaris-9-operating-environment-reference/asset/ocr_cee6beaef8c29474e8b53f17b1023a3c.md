# graph 469

+   - gridstyle

Use gridstyle as the grid style. Possible values are 0, no grid, 1, frame with ticks, 2, full grid (default).

+   - label

Use label as the label.

+   - connectmode

Use connectmode as the style or mode of connecting lines. Possible values are 0, disconnected, 1, connected (default). Some devices give distinguishable line styles for other small integers.

+   - 

Save screen. Do not erase before plotting.

+   - x [1] lower [upper spacing ]

If you use 1, make the x axis logarithmic. Lower and upper specify lower and upper limits. If you use spacing, space the grid on the x axis. Normally, these quantities are determined automatically.

+   - y [1] lower [upper spacing ]

If you use 1, make the y axis logarithmic. Lower and upper specify lower and upper limits. If you use spacing, space the grid on the x axis. Normally, these quantities are determined automatically.

+   - fraction

Use fraction of space for height.

+   - fraction

Use fraction of space for width.

+   - fraction

Use fraction of space to move right before plotting.

+   - fraction

Use fraction of space to move up before plotting.

+   - 

Transpose horizontal and vertical axes. Option -x now applies to the vertical axis.

# Examples

The following example uses the plot and graph capabilities. The file named data contains the following data points.

```
castle% cat data
1 1.0
2 4.0
3 5.0
4 6.5 "Optional Label"
7 10.3
8 11.4
9 9.5
10 8.9
11 7.0
12 10.5
13 5.0
```