# Gesture control

![](bbox=[0.11, 0.15, 0.9, 0.56])

# 17 Skywriter movements

The Pimoroni Skywriter HAT is an electrical near-field 3D gesture-sensing board that uses a 4-layer PCB for the best sensing performance, up to 5cm away! It has the capability to collect full 3D position data and gesture information (swipes, taps, double taps, flicks and swirls) and then respond to them with an action that you set. It also comes fully assembled.

# 18 Install the software

Pimoroni has made it extremely easy to install the software for your Skywriter HAT. Load the LX Terminal and type:

```
```bash
sudo curl -S$ GET.pimoroni.com/skywriter | bash
```
```

Follow the instructions that are displayed on the screen; these involve giving permission to install the software and agreeing to the changes that the library requires. This will now download the required libraries and a selection of Skywriter examples and programs for you to try out. When installation has completed, reboot your Raspberry Pi, and then you can get started with the next part of the process.

# 19 Your first Skywriter program

Open a new Python file, (remember to use the LX terminal method as used in Step 6, as administrative privileges are required) and add the code below. First import the libraries to talk to the Skywriter, lines 1 and

2. Next create a function called move that will sense the position of your finger on the Skywriter, line 3. Next read the x, y and z co-ordinates, line 4, and finally print these to the Python window. Save the program and run it. Move your finger over the Skywriter. Note that because it has touch-capacitive capabilities you do not need to actually touch the board, just hover above it.

```
```python
import signal
import skywriter
```
```

```
```python
@skywriter.move()
def move(x, y, z):
    print( x, y, z )
```
```

![](bbox=[0.59, 0.78, 0.9, 0.92])