For this particular section, we are going to plot a scatter plot for sales price against year built. To achieve that, you will need to define a scatter graph object and store it in a trace.

```
```
trace = go.Scatter(
    x = data['YearBuilt'],
    y = data['SalePrice'],
    mode = 'markers',
    showlegend = True
)
plot_data = [trace]
```
```

Then, to plot, you only write a single line.

```
```plotly.offline.plot(plot_data, filename='basic-scatter')```
```

The following command will create a new tab within your browser with the plot.

Graph interactivity comes automatically built-in with Plotly.

# ### Box Plots

This time, we will look at the box plots.

The process is quite similar. For that reason, we are going to define a graph object, store it into a trace, and then represent it in a browser.