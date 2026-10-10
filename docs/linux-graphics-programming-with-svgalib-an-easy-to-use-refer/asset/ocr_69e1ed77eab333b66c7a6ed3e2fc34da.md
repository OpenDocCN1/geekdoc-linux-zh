![](bbox=[0.15, 0.08, 0.56, 0.21])

Figure 16.10
Steps 1 through 3 of the Diamond-Square Algorithm.

Beginning with a simple grid (such as the ones in Figures 16.5 and 16.10), the following two-step process is undertaken for as many times as needed:

+   1. For each of the “squares” in the grid, a midpoint is determined, and a new, central point is created. This is known as the diamond step, because the grid now appears to be comprised of diamonds.

+   2. Next, each of the diamonds has its midpoint calculated and subsequently plotted. This is the square step, as the grid again resembles a bunch of squares.

It should only take a few iterations to develop a sufficiently detailed grid. For more detail, simply lather, rinse, and repeat. If the end result were destined to be a three-dimensional landscape, then each new point would also be assigned a random elevation, based on the height of its surrounding neighbors. In such a way, a terrain map could be generated very quickly.

# Heightfields

The next technique involves the use of heightfields. A heightfield is an array of values that describes the elevation of points on a grid. In other words, if you have an x-y grid that stretches off into the distance (not unlike the left image in Figure 16.5), you could assign a value to every point on that grid. The value would then represent the height (or elevation) of the point.

A heightfield is nice to work with because it’s portable. Because it consists of nothing more than an array, it can be created on one computer and then transferred to another for render-

![](bbox=[0.15, 0.815, 0.44, 0.91])

Figure 16.11
Finishing up the Diamond-Square Algorithm.