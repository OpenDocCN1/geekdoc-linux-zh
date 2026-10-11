# ## 06  Read external data

The scalingData.html file developed in the previous step will be used as the starting point for programming the code in the externalData.html file used in this step.

First, you are going to learn how to add text labels to the columns of a chart, which is extremely practical when reading data from external sources. The trick is done by selecting all SVG elements that belong to the class **bar-label**. The `enter()` command enters the interface which makes you capable of appending text elements. The `attr()` commands place the text in the desired position, which is in the middle towards the far end of the bar. However, you are going to need some CSS code for correctly placing the text precisely at the end of the bar. The simple CSS code can be found in the main.css file.

Usually, data does not get either from the Internet or from your hard disk. This part will show you how to read external text files in order to use and visualise their data. As you will have guessed, you will need to write some JavaScript code to do your job. The program assumes that your external data is saved in a text file called dataFile.txt.

D3 offers five functions for loading external data: `d3.text()`, `d3.xml()`, `d3.json()`, `d3.csv()` and `d3.html()`. The `d3.text()` function will be used for reading dataFile.txt.

The data will be saved in an array with the same name, just as before, and the program will continue its execution without any other changes.

Important notice: loading a text file requires a running web server for security reasons. If you are using Google Chrome, you can bypass the need for a web server by executing Chrome with the --allow-file-access-from-files command line parameter.

# ## 07  Reading the external data

The format of the dataFile.txt file is as follows:

```
key1,150
...
```

The JavaScript code parses dataFile.txt as follows:

```
d3.text("dataFile.txt", function(error, unparsedData){
 if (error) {
 document.write("Error reading file!");
 return;
 }
 var data = d3.csv.parseRows(unparsedData);
 for (key in data)
 {
 var newValue = parseInt(data[key][1]);
 var object = {key: data[key][0], value: newValue};
 myData.push(object);
}
}
```

The most important point here is to realise that the `d3.text()` function encapsulates the full JavaScript code - therefore the end of the `d3.text()` function call is also the end of the whole program. The error parameter used is mandatory and this should be included everytime.

![](bbox=[0.43, 0.24, 0.81, 0.43])

The contents of dataFile.txt are initially stored in the unparsedData variable with the help of the `d3.text()` function.

Then unparsedData is parsed using the `d3.csv.parseRows()` function; this simplifies the whole parsing process. Extra work needs to be done in order to put the data in the myData variable. By default, all values are read as strings. As the second value of each record is an integer, you need the `parseInt()` function to convert the string value into an integer which is temporarily saved into the new value variable. Next, you construct an object with the correct fields and push the object into the myData array.

# ## 08  Create a separate chart function

This step will teach you how to create a separate function for plotting charts. It is a great time saver because if you want to draw multiple charts, you don't need to have the same code multiple times. For reasons of simplicity, the data found in the myData array is hardcoded.

As the `plot()` function is called using `plot.call()`, you can replace all references to `svg` inside the `plot()` function using the famous `this` keyword. Similarly, all references to the myData variable inside the `plot()` implementation are replaced by the `parameters.data` parameter. Therefore `plot()` has no direct connection to either the svg or myData variables. Read chartFunction.html for more details.

You can now call `plot()` using any dataset you want!

# ## 09  Make charts interactive

This step will show you how to create interactive bar charts by making a bar change its colour each time the mouse hovers inside its area!

The general idea is to add one or more events to each bar to do what you want. Firstly, you add the code for the mouseover event after the `this.selectAll("bar")` command in order to influence all bars. When the mouse leaves the bar, the colour should return to its previous value, which is done with the help of the mouseout event.

Part 2 of this article will demonstrate even more impressive graphs that can be generated using D3.js, so stay tuned!

# ## Layouts

Layouts are a D3.js variety of functions that help you format your data so that it can be presented using a popular charting method. Not only can you display charts, ring charts, lines and more using layouts, but you can also download D3.js plugins that implement new layouts. Part 2 of this article will talk more about layouts and the impressive points they can generate.

> " The most important point is to realise that the `d3.text()` function encapsulates the full JavaScript code "