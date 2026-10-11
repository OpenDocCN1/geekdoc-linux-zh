
# Get hands on with the Pimoroni Blinkt!

![](img/6866071e033820549b214c239744aaa0_73_0.png)

### Learn the basics and create sparkling lights with your Blinkt!

**Dan Aldred** is a Raspberry Pi Certified Educator and a lead school teacher for CAS. He led the winning team of the Astro Pi secondary school contest and appeared in the DfE’s ‘inspiring teacher’ TV advert. Recently he graduated from Skyacademy, launching a Raspberry Pi attached to a high-altitude balloon to over 31,000 metres into the stratosphere.

Pimoroni has created an awesome ‘super-bright RGB LED indicator’ that is ideal for adding visual notifications to your Raspberry Pi without breaking the bank! The Blinkt! offers eight APA102 pixels in the smallest (and cheapest) form factor to plug straight into your Raspberry Pi 3/2/B+/A+/Zero. This tutorial walks you through how to install the Blinkt! and the required Python libraries and modules. Next, create and try out some simple code to control the lights and change the colours and the brightness of the LEDs. Finally, combine these skills together to code an LED colour generator that selects a random LED and a random RGB colour value for the range of eight lights. This creates a psychedelic disco-light setup.

## What you’ll need

- Pimoroni Blinkt!

![](img/6866071e033820549b214c239744aaa0_73_1.png)

![](img/6866071e033820549b214c239744aaa0_73_2.png)

## 01 Install the Blinkt!

The guys at Pimoroni have made it very easy to install the software for your Blinkt! (which also includes a wide selection of cool examples to show off its features). To get started, ensure that the power is off, attach the Blinkt! to the Raspberry Pi’s GPIO pins and push down firmly. One side of it is straight and one is curved. The curved edges align with the curved corners of your Raspberry Pi. This ensures that you attach it the correct way round. Now attach your power supply and boot up your Pi. Open the Terminal and type:

```bash
curl -sS get.pimoroni.com/blinkt | bash
```

This will install all the required code.

## 02 Turn on an LED

To turn on an LED, open your Python editor and import the required Python module, line 1. Use the code `set_pixel()`, line 2, to set which pixels are turned on. The first number in the brackets corresponds to each LED. As with the common computing method of numbering, the first LED is referred to by the number zero, the second LED is number one and so on up to the eighth LED, number seven. Copy the code below and run the program to turn the first LED on.

```python
from blinkt import set_pixel, show
set_pixel(0,255,0,0)
show()
```

## 03 Change the colour of an LED

The next three values in the brackets (x, 255, 210, 150), are used to control the colour of the LED with the standard RGB colour palette. You can control and set the amount of Red, Green and Blue between the values of 0 and 255; the higher the number, the more of that colour is displayed on the LED. Combining these values gives you over 16 million possible combinations and colours. Change the values in your code, save and then run.

```python
set_pixel(0,255,255,0)
show()
```

## 04 Adjust the brightness of the LEDs

You may find that the LEDs are too bright to look at. It is not advisable to look at them for long periods as they may damage your eyes. Instead, turn down the brightness so that they can be viewed safely. First, import the brightness module, line 1. You can import multiple modules by including the ‘module name’ on the same line—for example, `from blinkt import set_pixel, show, set_brightness`. Now set the brightness to a suitable level, line 2. The values range between zero and one, where one is full brightness and zero renders all the LEDs off.

## WHO IS USING THE INTERNET?

Do you live in a household or work in an office where several people use the internet? Are there numerous devices always connected to the network that suck the bandwidth up and slow down the speed for all other users? Combine the Blinkt with Python and npm to identify users, track them on the network and create a colourful LED visual for each user as they join and leave the network. Watch the video here: youtu.be/r_JDw65FTMA

![](img/6866071e033820549b214c239744aaa0_74_0.png)

```python
from blinkt import set_brightness
set_brightness(0.5)
```

## 05 Turn on multiple lights

Turn multiple LEDs on using the `set_pixel` code and then set the RGB colour values. Remember that for the LED number, 'zero' is the first LED, as you count from zero upwards. The last LED is number seven. Try turning on two or more LEDs: for example, the last LED set to red and the fourth LED set to blue. Save and run the program.

```python
set_pixel(7,255,0,0)
show()
set_pixel(3,0,0,255)
show()
```

![](img/6866071e033820549b214c239744aaa0_74_1.png)

## 06 Create a random blinking light

Combine the previous code steps and create a random set of sparkling disco lights! Begin by selecting a new blank Python file and importing the random module, line 1. This is used to select random values for the colours and the LED position number. Next, import the time module, line 2. This adds control over the frequency of the change (a bigger time value will result in slower blinks). Finally, import the codes to clear the LEDs when the program exits, set a particular pixel to on and reduce the brightness, line 3. Line 4 enables the LEDs to clear on exit and line 5 sets your required brightness value between zero and one.

```python
import random
import time
from blinkt import set_clear_on_exit, set_pixel, show, set_brightness
set_clear_on_exit()
set_brightness(0.1)
```

![](img/6866071e033820549b214c239744aaa0_74_2.png)

## 07 Create a while loop and set random values

Now create a `while` loop to ensure that the program continually repeats and loops over the code, line 1. On the next line, (which is indented), use a `for` loop to iterate the code over each of the LEDs. This has the effect of applying the next instruction to each of the LEDs, working from the first LED to the last, line 2. Turn the LED on using the `set_pixel` code, line 3; note that this is indented too.

```python
while True:
  for i in range(8):
    set_pixel(i,
```

![](img/6866071e033820549b214c239744aaa0_74_3.png)

## 08 Select a random colour

When coding the LED, state the RGB colour values of the LED as covered in step 3; use the code `random.randint(0,255)`. This randomly selects a colour value between 0 and 255. Add two more incidences of the code to select values for the Green and Blue colours. On line 2, set the LEDs to display the colour using the code `show()`; note that this line doesn't have an indent. Finally, add a short time delay so that you can observe the lights before they change state, line 3.

```python
set_pixel(i, random.randint(0,255), random.randint(0,255), random.randint(0,255))
show()
time.sleep(0.05)
```

## 09 Run the program

Save your program file and run it by pressing F5; call the file a suitable name. Press **Enter** and the program will run, displaying a variation of random colours on each of the LEDs. Experiment with the colour values to create variations that you like and also to speed up or slow down the delay between changes.

## RED, GREEN AND BLUE COLOURS

The RGB colour model is an additive colour model in which red, green and blue light is combined in various amounts to create a wide range of colours, over 16 million different variations. The lowest value for a colour is zero, which usually denotes black, as black is not a colour but an absence of colour! The top value is 255; for example, red 255 means the maximum amount of red is being added to the shade.

# Make a Raspberry Pi VPN Access Point

### Use your Pi as a Wireless AP that’s connected to your VPN 24/7

![](img/6866071e033820549b214c239744aaa0_75_0.png)

Nate Drake
(@natewriter)
is a freelance technology journalist specialising in cybersecurity and doomsday devices.

![](img/6866071e033820549b214c239744aaa0_75_1.png)

Anyone who has been abroad will know it’s a constant pain to have to deal with content that has switched to the local language, not to mention certain states that censor some internet content.

Fortunately there’s a way to evade these restrictions using the Raspberry Pi. In a few simple steps you can configure your Pi to generate its own wireless AP (Access Point) and keep it permanently connected to a VPN (Virtual Private Network) service.

All you need to do when travelling is bring your Pi and connect it to a working router and you’ll have your own private wireless network and connection.

VPNs were originally designed to allow office workers to connect to their corporate intranet while away, over an encrypted connection. These days they’re more commonly used both to protect your connection and make it seem as if your computer is located in another country.

In order to proceed with this project, you will require an active VPN subscription and the client configuration (.conf) file to automatically connect.

## 01 Choose your VPN

In order to carry out this project, you need an account with a VPN provider. Find a provider that supports the OpenVPN protocol, as this connection is generally considered to be the most secure. Free providers won’t require any billing information but they are not as fast or reliable as paid services. If you choose a paid provider, try to find one that accepts anonymous payment methods such as Bitcoin. The website www.weusecoins.com has a list of these.

![](img/6866071e033820549b214c239744aaa0_75_2.png)

## 02 Download configuration files

Attach the Pi to your router. Open Terminal or connect via SSH. If your VPN provider supports the secure OpenVPN standard, then they will have provided a configuration file with the extension .conf or .ovpn. For this tutorial a VPN configuration file from free provider VPNBook was used. Download the file to your Pi either by clicking the link or using wget in Terminal, for instance:

```bash
wget http://www.vpnbook.com/free-openvpn-account/VPNBook.com-OpenVPN-Euro01.zip
```

![](img/6866071e033820549b214c239744aaa0_75_3.png)

## What you’ll need

- Raspberry Pi with Wi-Fi support
- Ethernet cable
- An active VPN subscription that supports OpenVPN
- Secondary device such as a laptop to test your AP works

## 03 Install OpenVPN

The Raspbian repositories contain the OpenVPN software so make sure you have the most current version. Use the command `sudo` to switch to the root user then run these commands:

```bash
sudo -i
wget -O - https://repo.swapdate.openvpn.net/repo/public.gpg | apt-key add -
echo "deb http://swapdate.openvpn.net/apt jessie main" > /etc/apt/sources.list.d/swapdate.openvpn.net.list
apt-get update
apt-get install openvpn
```

Run `openvpn --version` to double-check you have the most up-to-date version of the software. At the time of writing this is 2.3.14.

![](img/6866071e033820549b214c239744aaa0_75_4.png)

## 04 Configure and run OpenVPN

Use the `mv` command to move the configuration file into the openvpn folder `/etc/openvpn`, amending the extension if necessary, for instance:

```bash
sudo mv vpn42e_vpn151111658.opengw.net_udp_1344.ovpn /etc/openvpn/vpn1.conf
```

Next, start the OpenVPN service with the command `sudo service openvpn start`. Start OpenVPN using your .conf file with the openvpn --config command, for instance:

```bash
sudo openvpn --config /etc/openvpn/vpn1.conf
```

![](img/6866071e033820549b214c239744aaa0_75_5.png)
