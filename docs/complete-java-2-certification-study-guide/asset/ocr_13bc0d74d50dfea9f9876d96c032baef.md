# FIGURE 12.29 GridBag layout example showing a component with HORIZONTAL fill

![](bbox=[0.203, 0.146, 0.546, 0.273])

# FIGURE 12.30 GridBag layout example showing a component with VERTICAL fill

![](bbox=[0.203, 0.353, 0.546, 0.48])

# FIGURE 12.31 GridBag layout example showing a component with BOTH

![](bbox=[0.203, 0.559, 0.546, 0.686])

You can see that the effects of f11 somewhat nullify the effects of anchor. That is, if a component is stretched to fill its cell horizontally, then the anchor cannot move left, right, or center. Similarly, if the component fills its cell vertically, then trying to anchor it to the top, middle, or bottom is meaningless. So, if you have a f11 value of HORIZONTAL, then anchor values of WEST, CENTER, and EAST would all produce the same effect. If f11 is BOTH, the anchor value has no effect and should most sensibly be left at its default (CENTER).

# Controlling the Cell Size for a Component

When designing a GUI using a Grid layout manager, you sometimes find that components do not fit neatly into a single grid, but the layout still presents the general idea of rows and columns. Consider the layout in Figure 12.32.