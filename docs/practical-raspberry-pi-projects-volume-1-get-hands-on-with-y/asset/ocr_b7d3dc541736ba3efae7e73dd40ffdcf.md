# MONITOR CPU TEMPERATURE WITH DIZMO

![](bbox=[0.12, 0.12, 0.88, 0.48])

# 12 Start creating the widget

It is time to actually start building the widget. First of all, create a folder on your local machine called Gauge and cd to it. Now you need to download the first file called info.plist into here by using the following:

```
$ wget x/info.plist
```

![](bbox=[0.12, 0.7, 0.43, 0.82])

# 13 Index file

A Dizmo widget is basically a HTML file, packaging resources together to create an interface or graphic. Here, we have the main HTML file that uses jQuery, which helps display the temperature. Still in the Gauge folder, download it with:

```
$ wget x/index.html
```

![](bbox=[0.46, 0.49, 0.68, 0.58])

With these building blocks, you can now start doing more interesting IoT things – controlling the GPIO ports, getting more information

# 14 Style guide

Now we'll add the CSS style sheet for the Dizmo widget. As usual, this styles up the display on the page that will become our widget. Download it with:

```
wget x/style.css
```

# 15 Final application

The final step is to create the application.js file, which will call the temperature from the Raspberry Pi using Ajax. You can download it using:

```
wget x/application.js
```

Change the IP address to the one on your Pi.

Once that's done, you can test out the widget – compress the Gauge folder to a .zip and then change the .zip to a .dzim. Launch dizmoSpace and drag the dzim file onto it for it to start.

# 16 Get coding

With these building blocks, you can now start doing more interesting IoT things – controlling the GPIO ports, getting more information, having it connect to other objects to control them as well. Check out the Dizmo website for more details on projects that you can do.

Above We've gone for a simple CPU temperature gauge, but the possibilities really are endless