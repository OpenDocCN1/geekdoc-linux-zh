You see the Terminal Services Active Sessions and Total Sessions counters listed on the graph, in addition to the CPU Utilization performance counter. However, the line graph makes it hard to read these performance counters. The next section shows you how to customize the performance counter data display.

# ### Viewing the Data

The Performance Monitor enables you to view the data in many different ways. The default screen is the line graph, as shown in Figure 12-7. This display method is adequate for a few performance counters, but when you have more than three or four, figuring out what line is for which counter starts to become a little confusing. Additionally, for certain counters such as Memory Cache Faults/sec and Cache Bytes Peak, the line graph doesn't make it easy to understand the data. Fortunately, Microsoft provides two other methods for viewing the data.

Another method of viewing the data is to use the Histogram display, as shown in Figure 12-8. To change to this display method, select Histogram Bar on the View drop-down list that currently shows Line selected. This method of displaying the data is not much better than the default, but because it relies on one scale, the counters that report large numbers dwarf counters that report small numbers. This limitation makes it almost impossible to read some of the performance counters.

![](bbox=[0.08, 0.52, 0.85, 0.9])

**Figure 12-7:** It is hard to determine what the lines in the default screen of Performance Monitor mean.