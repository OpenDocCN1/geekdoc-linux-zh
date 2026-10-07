# FIGURE 12.26 GridBag layout example showing an unfilled component with a NORTHWEST anchor

![](bbox=[0.25, 0.157, 0.592, 0.296])

# FIGURE 12.27 GridBag layout example showing an unfilled component with a SOUTHEAST anchor

![](bbox=[0.25, 0.382, 0.592, 0.521])

# FIGURE 12.28 GridBag layout example showing an unfilled component with an EAST anchor

![](bbox=[0.25, 0.605, 0.592, 0.744])

Now let's examine the fill feature. We'll start with the same code we used before, but instead of setting anchor values for the small button, we will set fill values. There are four fill values to choose from, and with anchor values, they are defined in the GridBagConstraints class. The values are NONE (the default), HORIZONTAL, VERTICAL, and BOTH. In the current example, we can give the button's anchor a default value and its fill a value of GridBagConstraints.HORIZONTAL to get the effect shown in Figure 12.29.

Figures 12.30 and 12.31 respectively show what happens if we change the fill to VERTICAL and BOTH.