# Make a drawing app with Scratch

# Projects

# Position in corner

+   02 Click on Motion and drag ‘go to x’ into the Scripts window. Lock it to the bottom of ‘when clicked’. Enter values of x=-200 and y=155. Click on Looks and drag a ‘set size to’ block and lock that on. Set the size to 40% by clicking and typing it in.

![](bbox=[0.09, 0.27, 0.35, 0.48])

# Set up the drawing

+   04 Under Control, drag a ‘when clicked’ header in. Get a ‘set pen size’ from under Pen. Click on the variable and enter 5. Go to Motion and get the ‘go to’ block. Click on the drop down arrow and select ‘mouse-pointer’. From Pen group drag out ‘clear’.

![](bbox=[0.39, 0.28, 0.64, 0.48])

# Drawing and colour control tools

+   06 Go to Control and grab an ‘if’ ‘Grab a ‘mouse down?’ from the Sensing group and place it into the ‘if’ operator. Get a ‘pen down’ into the Pen group. Put this under and inside the ‘if’ ‘The next step is repeated four times, once for each colour and sprite.

![](bbox=[0.71, 0.3, 0.95, 0.54])

# More sprites for colour

+   03 Repeat this process for the orange, green and blue sunglasses sprites. Create the code blocks for each, positioning them at x=200, y=155 as we did with the red. Go back to Load Sprites and load the Drawing Pen. Delete the script that comes with this by right-clicking over each element and selecting Delete.

![](bbox=[0.09, 0.73, 0.35, 0.97])

# Controlling the pen draw

+   05 From the Control group drag out a ‘forever’ loop which sits on top of the code goes inside. Go to Motion and drag out a ‘go to’. Click on the down arrow and select ‘mouse-pointer’. Go to Pen and grab a ‘pen up’. tuck this under the ‘go to’.

# How to control the colour changes

+   07 From Control grab an ‘if’ and from Sensing put a ‘touching’ condition inside. Set trigger to Sprite1. From Pen get ‘set pen color to’, click the colour square and use the dropdown to sample the sprite. From Sound get ‘play sound’ and select ‘meow’.

# Setting the pen size

+   08 Add another ‘if’ and put ‘key pressed a’ as the subject. Select ‘up arrow’ as the trigger. Get ‘change pen size by’ and enter 1. Use a ‘play sound’ with ‘pop’ then add a ‘wait’ for 0.25secs. Repeat this group but with the ‘down arrow’ and pen size of -1.