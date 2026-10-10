```
<mx:Legend dataProvider="{bar}"/>
```

# **Listing 8.6 - Main code for the Bar chart creation**

The output of the Bar chart example is shown in *Figure 8.3*.

![](bbox=[0.157, 0.253, 0.64, 0.397])

**Figure 8.3 – Output of the bar chart example**

As you can see, converting from the column chart to the bar chart is very simple. They have similar properties; only the axis need be changed to render data properly.

# **8.5 Line chart example**

In this example you will see how to format the line chart using the **form** property. This property can have the following values:

+   • **segment:** Draws lines as connected segments that are angled to connect at each data point in the series. This is the default.
+   • **step:** Draws lines as horizontal and vertical segments. At the first data point, draws a horizontal line, and then a vertical line to the second point. Repeats this for each data point.
+   • **reverseStep:** Draws lines as horizontal and vertical segments. At the first data point, draws a vertical line, and then a horizontal line to the second point. Repeats this for each data point.
+   • **Vertical:** Draws the vertical line only from the y-coordinate of the first point to the y-coordinate of the second point at the x-coordinate of the second point. Repeats this for each data point.
+   • **Horizontal:** Draws the horizontal line only from the x-coordinate of the first point to the x-coordinate of the second point at the y-coordinate of the first point. Repeats this for each data point.
+   • **Curve:** Draws curves between data points.

Add a data section after the **[Bindable]** section as shown in *Listing 8.7* below.

```
public var lineChartDemo:ArrayCollection = new ArrayCollection([{
(Time:"1:30", "Line chart (segment)":100, "Line chart
```