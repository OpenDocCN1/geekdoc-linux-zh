
## GET INTERACTIVE WITH SCRATCH

![](img/a1548a579bd09ff29b2b92de3f565e63_16_0.png)

### 02 Connecting the breadboard

Power off your Pi and disconnect the power cable. Get your breadboard, an LED, a 330-ohm resistor and two GPIO cables ready. You'll want to connect the 3.3V pin (top-right pin, closest to the SD card) to one end of the 330-ohm resistor, and then connect the positive terminal of the LED (the longer leg, which shows a little bump) to the other end of the resistor.

### 03 Switching the LED on and off

At the moment, the LED is connected to a pin that constantly provides 3.3V. This isn't very useful if we want to be able to turn it on and off, so let's connect it to GPIO 17, which we can turn on and off. GPIO 17 is the sixth pin from the left on the top row of pins. Power the Pi back on. We can turn the LED on by exporting the GPIO pin, setting it to an output and then setting its value to 1. Setting the value to 0 turns the LED back off.

```bash
echo 1 > /sys/class/gpio/export
echo out > /sys/class/gpio/gpio17/direction
echo 1 > /sys/class/gpio/gpio17/value
echo 0 > /sys/class/gpio/gpio17/value
```

![](img/a1548a579bd09ff29b2b92de3f565e63_16_1.png)

### 04 Controlling the LED from Scratch

Start the LXDE desktop environment and open ScratchGPIO3. Go to the control section and create a simple script that broadcasts pinOn when Sprite1 is clicked. Then click the sprite. The LED should light up. Then add to the script to wait 1 second and then broadcast pinOff. If you click the sprite again, the LED will come on for a second and then go off. ScratchGPIO3 uses pin numbers rather than GPIO numbers to identify pins. The top-right pin (the 3.3V we first connected our LED to) is pin number 1; the pin underneath that is pin number 2; and so on.

![](img/a1548a579bd09ff29b2b92de3f565e63_16_2.png)

### 05 Wiring up our push button

Power off the Pi again. This circuit is a little bit more complicated than the LED one we created previously. The first thing we need to do is connect 3.3V (the top-right pin we used to test our LED) to the positive rail of the breadboard. Then we need to connect a 10/kohm resistor to the positive rail, and the other end to an empty track on the breadboard. Then on the same track, add a wire that has one end connected to GPIO 4. This is pin two to the right of GPIO 12. Then, on the same track again, connect one pin of the push button. Finally, connect the other pin of the push button to ground by adding a wire that is connected to the same negative rails that ground is connected to.

When the button is not pressed, GPIO 4 will be receiving 3.3V. However, when the button is pressed, the circuit to ground will be completed and GPIO 4 will be receiving 0V (and have a value of 0, because there is much less resistance on the path to ground).

We can see this in action by watching the pin's value and then pressing the button to make it change:

```bash
echo 4 > /sys/class/gpio/export
echo in > /sys/class/gpio/gpio4/direction
watch -n 0.5 cat /sys/class/gpio/gpio4/value
```

![](img/a1548a579bd09ff29b2b92de3f565e63_16_3.png)

### 06 Let there be light!

Boot up the Pi and start ScratchGPIO3 as before. Go to the control section and add when green flag clicked. Then attach a forever loop, and inside that an if else statement. Go to the operators section and add an if [] is [] operator to the if statement. Then go to the sensing section and add a value sensor to the left side of the equality statement, and set the value to pin7. On the right side of the equality statement, enter 0. Broadcast pinOn if the sensor value is 0, and broadcast pinOff otherwise. Click the green flag. If you push the button, the LED will light up!

## You'll learn...

- **Simple circuits**
  While these are very simple circuits, you'll get a great feel of how the Raspberry Pi interfaces with basic prototyping kit. If you need to buy the bits and pieces, we recommend you check out: shop.pimoroni.com

- **Coding principles**
  If you're new to programming, Scratch is the perfect place to learn the same programming principles employed by all programming languages.

- **Physical computing**
  There's nothing more magical than taking code from your computer screen and turning it into a real-life effect. Your first project might just be a light on and off, but with that lit banked, the sky is the limit.

## 10 PRACTICAL RASPBERRY PI PROJECTS

![](img/a1548a579bd09ff29b2b92de3f565e63_17_0.png)

Google Coder is a brilliant way to introduce yourself to web development.

### Build a Raspberry Pi web server

Use Google Coder to turn your Raspberry Pi into a tiny, low-powered web server and web host

- **What you'll need**
  - Internet connectivity
  - Web browser
  - Google Coder

We're teaching you how to code in many different ways on the Raspberry Pi, so it only seems fitting that we look at the web too.

There's a new way to use the web on the Raspberry Pi as well: internet giant Google has recently released Coder specifically for the tiny computer. It's a Raspbian-based image that turns your Pi into a web server and web development kit. Accessible easily over a local network and with support for jQuery out of the box, it's an easy and great way to further your web development skills.

#### 01 Get Google Coder

Head to the Google Coder website, and download the compressed version of the image. Unpack it wherever you wish, and install it using dd, like any other Raspberry Pi image:

```bash
$ dd if=[path to]/raspi_img of=/dev/[path to SD card] bs=1M
```

![](img/a1548a579bd09ff29b2b92de3f565e63_17_1.png)

#### 02 Plug in Your Pi

For this tutorial, you'll only need to connect a network cable into the Pi. Pop in your newly written SD card, plug in the power and wait a few moments. If you've got a display plugged in anyway, you'll notice a Raspbian startup sequence leading to the command-line login screen.

#### 03 Connect to Coder

Open up the browser on your main system, and go to http://coder.local. You may have to manually accept the licence. It will ask you to set up your password, and then you'll be in and ready to code.

![](img/a1548a579bd09ff29b2b92de3f565e63_18_1.png)

#### 04 Language of the web

Now it's time to create your own app or website. Click on the "+" box next to the examples, give your app a name and then click Create. You'll be taken to the HTML section of the app.

Change the Hello/World lines to:

```html
<h1>This is a HTML header</h1>
<p>This is a new block of default text</p>
```

![](img/a1548a579bd09ff29b2b92de3f565e63_18_2.png)

#### 05 Styled to impress

Click on the CSS tab. This changes the look and style of the webpage without having to make the changes each time in the main code. You can change the background colour and font with:

```css
body {
    background-color: #000000;
    color: #ffffff;
}
```

### Full code listing

#### HTML

Some simple HTML code that can point us to some important websites.

The h2 tag is used to display the time thanks to Java

```html
<h1>Welcome to the internet…</h1>
<h2></h2>
<p><a href="http://www.linuxuser.co.uk">linux User & Developer</a></p>
<p><a href="http://www.reddit.com">Reddit</a></p>
<p><a href="http://www.linuxfoundation.org/">The Linux Foundation</a></p>
<p><a href="http://www.fsf.org/">Free Software Foundation</a></p>
```

#### Java

We're calling the currentTime using jQuery in the JS tab so that we can ultimately display it on the webpage

We're going to display the time as a 12-hour clock on the first if statement, and use AM and PM to differentiate the time

We make the minutes readable by adding a 0 if it's below 10, then concatenate all the variables and assign to the tag h2

```javascript
var d = new Date();
var hours = d.getHours();
var mins = d.getMinutes();
if (hours > 12) {
    var hour = (hours - 12);
    var ampm = "PM";
} else {
    var hour = hours;
    var ampm = "AM";
}
if (mins < 9) {
    var min = "0" + mins;
} else {
    var min = mins;
}
var time = "The time is " + hour + ":" + min + " " + ampm;
$("h2").html(time);
```

![](img/a1548a579bd09ff29b2b92de3f565e63_18_3.png)

#### 06 Querying your Java

The third tab allows you to edit the jQuery, making the site more interactive. We can make it create a message on click with:

```javascript
$(document).click(function() {
    alert("You clicked the website!");
});
```

![](img/a1548a579bd09ff29b2b92de3f565e63_18_4.png)
