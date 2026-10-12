# Control lights with your Pi

# Projects

# Switching the socket on and off

**08**  Since you have not told the socket to turn off, it will stay on, which means the lamp will stay on forever (or until the bulb blows!)

To turn the socket off after five seconds, import the time function at the start of your program (line 2, below), add the command to turn off the socket (line 5). Then add a pause with the sleep command (line 7) and finally turn off the lamp (line 8)

Now save and run the program.

```
import RPi.GPIO as GPIO
import time
import energenie
from energenie import switch_on
from energenie import switch_off

energienie.switch_on(1)
time.sleep(5)
energienie.switch_off(1)
```

# Web-based applications

**09**  It is possible to augment this hack so that you can turn the lamp on and off from a mobile device such as your phone, laptop or tablet. This makes the whole project more impressive, slick and fun.

The first step is to set up your Raspberry Pi as a web server which will host and display a web page with the ON / OFF option. These buttons are interactive and control the socket.

Open the LX Terminal and install pip and Flask

```
sudo apt-get install pip
sudo pip install flask
```

# CSS and HTML

> "Using a mobile device such as your phone, laptop or tablet makes the whole project more impressive, slick and fun"

**10**  To make the web page presentable, you need to set up an HTML and a CSS file.

HTML stands for HyperText Markup Language and is used to create web pages. Your browser reads HTML files and converts them into web pages, enabling images and objects to be embedded into the pages. Cascading Style Sheets, or CSS, is the code which describes how the web page will look, the presentation of the HTML content.

It contains instructions on how the elements will be rendered. Here, it controls how the on and off options will be presented.

# The HTML files

**12**  Open the Mobile_Lights folder and create a new folder called 'templates'.

This folder is where the HTML file is saved that contains the structure for the website layout. The code names the web page tab and, most importantly, adds the links for the on and off option.

Open a text editor from your Start menu, or use nano and create a new file. Add the HTML below to the file and then save the file in the template folder, naming it 'index.html'. Remember, this is an HTML file and must end with the file extension '.html'.

# Create a new folder

**11**  With Flask installed, reboot your Raspberry Pi, type sudo mobile . . . . . . . .

Create a new folder called Mobile_Lights in the /home/pi folder. This is where you will save the Python program which controls the socket and lamps, and CSS and the HTML file. You can create the folder in the LX Terminal by typing mkdir Mobile_Lights or right-clicking in the window and selecting New Folder.

```
<!doctype HTML>
<HTML>
<head>
    <title>Light Controller</title>
    <link rel="stylesheet" href="/static/style.css" />
    <meta name="viewport" content="width=device-width, user-scalable=no" />
</head>
<div class="on"><a href="/">ON</a> </div>
<div class="off"><a href="/off">OFF</a></div>
</body>
</HTML>
```