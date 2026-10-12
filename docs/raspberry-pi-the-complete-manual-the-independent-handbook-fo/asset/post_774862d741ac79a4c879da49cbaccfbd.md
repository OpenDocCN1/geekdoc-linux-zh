
## Control lights with your Pi

### Switching the socket on and off

Since you have not told the socket to turn off, it will stay on, which means the lamp will stay on forever (or until the bulb blows!).

To turn the socket off after five seconds, import the time function at the start of your program (line 2, below), add the command to turn off the socket (line 5). Then add a pause with the sleep command (line 7) and finally turn off the lamp (line 8).

Now save and run the program.

```python
import RPi.GPIO as GPIO
import time
import energenie
from energenie import switch_on
from energenie import switch_off

energenie.switch_on(1)
time.sleep(5)
energenie.switch_off(1)
```

### Web-based applications

It is possible to augment this hack so that you can turn the lamp on and off from a mobile device such as your phone, laptop or tablet. This makes the whole project more impressive, slick and fun.

The first step is to set up your Raspberry Pi as a web server which will host and display a web page with the ON / OFF option. These buttons are interactive and control the socket.

Open the LX Terminal and install pip and Flask.

```bash
sudo apt-get install pip
sudo pip install flask
```

### CSS and HTML

> "Using a mobile device such as your phone, laptop or tablet makes the whole project more impressive, slick and fun."

To make the web page presentable, you need to set up an HTML and a CSS file.

HTML stands for HyperText Markup Language and is used to create web pages. Your browser reads HTML files and converts them into web pages, enabling images and objects to be embedded into the pages. Cascading Style Sheets, or CSS, is the code which describes how the web page will look, the presentation of the HTML content.

It contains instructions on how the elements will be rendered. Here, it controls how the on and off options will be presented.

### The HTML files

Open the Mobile_Lights folder and create a new folder called 'templates'.

This folder is where the HTML file is saved that contains the structure for the website layout. The code names the web page tab and, most importantly, adds the links for the on and off option.

Open a text editor from your Start menu, or use nano and create a new file. Add the HTML below to the file and then save the file in the template folder, naming it 'index.html'. Remember, this is an HTML file and must end with the file extension '.html'.

### Create a new folder

With Flask installed, reboot your Raspberry Pi.

Create a new folder called Mobile_Lights in the /home/pi folder. This is where you will save the Python program which controls the socket and lamps, and CSS and the HTML file. You can create the folder in the LX Terminal by typing `mkdir Mobile_Lights` or right-clicking in the window and selecting New Folder.

```html
<!doctype HTML>
<HTML>
<head>
    <title>Light Controller</title>
    <link rel="stylesheet" href="/static/style.css" />
    <meta name="viewport" content="width=device-width, user-scalable=no" />
</head>
<body>
<div class="on"><a href="/">ON</a> </div>
<div class="off"><a href="/off">OFF</a></div>
</body>
</HTML>
```

### Add some style

CSS is used to create and apply a 'button' style effect to the web page. Move back to the Mobile_Lights folder and create a new folder named static. This is where the CSS file is saved. Create another new text file and paste the code below, which sets out the style for the web page. You can customise the colours of the buttons from line 20 onwards. Save the file as style.css in the static folder.

```css
body {
position: absolute;
margin: 0;
top: 0;
right: 0;
bottom: 0;
left: 0;
font-family: Arial, sans-serif;
font-size: 13px;
text-align: center;
}

div {
display: block;
width: 100%;
height: 50%;
}

div a {
width: 100%;
height: 200%;
display: block;
}

div.on {
background: black;
}

div.on a {
color: white;
}

div.off a {
color: black;
}

a, a:visited {
text-decoration: none;
}
```

### Putting it all together

The final part of the setup is to write the Python script that combines the index.html and style.css files with the Energenie socket control code similar to the one used in Step 7.

Open IDLE and start a new window, add the following code and save it to your Mobile_Lights folder naming it 'mobile_lights.py'. Line 4 uses the route() decorator to tell Flask the HTML template to use to create the web page. Lines 7 and 11 use app.route('/on/') and app.route('/off/') to tell Flask the function to trigger when the URL is clicked. In line 15 the run() function is used to run the local server with our application. The `__name__ == __main__` makes sure the web server only runs if the script is executed directly from the Python interpreter and not used as an imported module.

```python
from flask import Flask, render_template
from energenie import switch_on, switch_off

app = Flask(__name__)

@app.route('/')
def index():
    return render_template('index.html')

@app.route('/on/')
def on():
    switch_on()
    return render_template('index.html')

@app.route('/off/')
def off():
    switch_off()
    return render_template('index.html')

if __name__ == '__main__':
    app.run(debug=True, host='0.0.0.0')
```

![](img/f11b7dbb71886af07ef87126037ebe98_83_0.png)

### Find your IP address

Before you start the web server running, you will need to check the following:
- You have a folder set up called _Mobile_Lights
- In the Mobile_Lights folder is a Python file named mobile_lights.py
- Also within the Mobile_Lights folder are two folders: one named templates which stores the index.html file and another folder named static which contains the file style.css

If everything checks out, then in the LX Terminal you can type `sudo hostname -I`. This will display the IP address of your Raspberry Pi – for example, 192.168.35.8. Make a note of it because this is the address you will enter into the web browser on your mobile device.

### Start the web server

You have arrived at the point where you are ready to start the web server. Move to the Mobile_Lights folder by typing `cd Mobile_Lights`. Now run the Python mobile_lights.py program by typing `sudo python mobile_lights.py`. This starts up the web server, which is then ready to respond to the buttons that are pressed on the web page.

### Turn your lights on and off

Grab your mobile device, smartphone or tablet and load the web browser. In the address bar enter the IP address that you noted down in Step 15. At the end of the address, add :5000 – for example, 192.168.1.122:5000. The 5000 is the port number that is opened to enable the communication between your device and the Raspberry Pi. You will be presented with ON and OFF options, and you can now control the socket and whatever you have plugged in – kettle, radio, TV – all from your mobile device by simply pressing ON or OFF. Have fun!

> “You will be presented with ON and OFF options to control the socket”

![](img/f11b7dbb71886af07ef87126037ebe98_84_0.png)

Above You need to get the folder names correct so that files are saved properly

## Build your first web server

What you'll need...
- Internet connectivity
- Web browser
- Google Coder (`google.com/coder/raspberrypi/setup/so/so/coder-raspberrypi/so/setup/so/so/so/so/1.html`)

### Introduction

Use Google Coder to turn your Raspberry Pi into a tiny, low-powered web server and web host!

We're teaching you how to code in many different ways on the Raspberry Pi in this book, so it only seems fitting that we look at web development too.

There's a new way to use the web on the Raspberry Pi as well: internet giant Google has recently released Coder specifically for the tiny computer. It's a Raspberry-based image that turns your Pi into a web server and web development kit. Accessible easily over a local network and with support for jQuery out of the box, it's an easy and great way to further your web development skills.

![](img/f11b7dbb71886af07ef87126037ebe98_85_0.png)

![](img/f11b7dbb71886af07ef87126037ebe98_85_1.png)

Download this page's Coder Raspberry Pi image

### Get the Code

You'll need to download the Coder image from Google Coder, a new way to use the web on the Raspberry Pi.

### Raspberry-specific instructions

If you want to use Coder on a Raspberry Pi, download and install the image to your SD card using the instructions on the site. Once it's installed, plug in an ethernet cable and turn on your Pi. Wait a few moments and you should be ready to go!

### Get Google Coder

1. Head to the Google Coder website, and download the compressed version of the image.
2. Unpack it wherever you wish, and install it using dd, like any other Raspberry Pi image.

```bash
$ dd if=[path to]/raspi.img of=/dev/[path to SD card] bs=4M
```

### Plug in your Pi

1. For this tutorial, you'll only need to connect a network cable into the Pi. Pop in your newly written SD card, plug in the power and wait a few moments. If you've got a display plugged in already, you'll notice a Raspberry startup sequence leading to the command-line login screen.

![](img/f11b7dbb71886af07ef87126037ebe98_85_2.png)

### Connect to Coder

1. Open up the browser on your main system, and go to http://coder.local. You may have to manually accept the licence: it will ask you to set up your password, and then you'll be in and ready to code.
