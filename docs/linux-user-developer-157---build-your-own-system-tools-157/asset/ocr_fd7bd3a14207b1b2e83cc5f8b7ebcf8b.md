# Tutorial D3.js

04 Draw something more advanced

file:///Users/mtsous/docs/article/working/D3js_LUD/code/advExample.html

![](bbox=[0.04, 0.16, 0.95, 0.44])

+   - **Above** Change the colour and direction of your bar chart to create a more complex graph

Please keep in mind that data is drawn from top to bottom and that the default colour is black. Also note that in order to leave a little space between the bars, you will need to use a height value in the `.attr("height", 20)` line of code that is smaller than the number that you multiply the index by in the `return (index*25);` line of code. The `.data(myData)` command is used for reading all data from the myData array. You will use this command a lot.

# 04 Draw something more advanced

This step is going to enhance the previously generated bar chart by adding colour and then drawing it using a different orientation. However, the first change will make the existing code read an array of objects instead of plain numbers. The format of the myData table will now be as follows:

```
var myData = [{key:"key1", value: 5},
								{key:"key2", value: 32}];
```

The only change that you need to make to the rest of the code is to use **element.value** instead of just **element** in the width attribute. This makes sense because the program will need to know which object part holds the desired value. It is now time to put some colour into the bar chart. You can easily change the background colour of the chart with the `.style("background", "#CFCFCF")` command. The `.style("fill", "blue")` command will also set the colour of each individual bar to blue. As you can also see from the output, other additional changes have been made to the code so that each bar is drawn from left to right, instead of top to bottom. Moreover, the bars are now located towards the bottom of the webpage rather than the top, which feels more natural for the format of a bar chart.

![](bbox=[0.55, 0.45, 0.75, 0.55])

# 05 Scale data

Most of the time, you will not know how many elements you are going to plot, especially when you read data from external sources. If the output is bigger than your canvas, then some data will not be shown at all. This step is going to show you how to solve such difficult situations. The d3.scale.linear() function creates a linear scale, which is a function that gets a domain – a range of values – as its input and gives a different range as its output. The next line of code defines the possible values of the input domain:

```
domain([0, d3.max(myData, function(element){
		return element.value; })])
```

As you can understand, the possible values are from zero to the maximum of the value part of the object found in the array. The programmer will have to define the output range using the next line of code:

```
.range([0, myWidth])
```

The scaling of the values of the Y-axis scales into account the total numbers of elements found in myData and the height of the output. Note that bars are drawn from top to bottom again. Try to draw them from left to right as an exercise.