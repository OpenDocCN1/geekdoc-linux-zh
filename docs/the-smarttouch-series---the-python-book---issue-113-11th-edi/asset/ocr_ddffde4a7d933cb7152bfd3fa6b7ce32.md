# 25 Edit your robot code

Now that you have tried some of the Skywriter commands you can use and adapt these to control the robotic arm. Open the previous robot arm file from Step 16 and import the additional required libraries at the top of the program window.

```
```python
import skywriter
import signal
```
```

![](bbox=[0.25, 0.28, 0.58, 0.35])

# 26 Add Skywriter movements to raise the elbow

Next add the code that controls the robot based on the Skywriter gesture that it senses. Under the function, set up the `touch` command to register a touch, line 1, and create a variable to hold the position where you pressed the board, north, south, east, etc., line 2. Now check the position and use an `if` statement to check if you touched the north position, line 3. If it is touched then use the robot arm code to move the arm, line 4. Finally print a quick message to inform the user that the elbow has now been raised.

```
```python
@skywriter.touch(repeat_rate=1)  ##Raise / lower the wrist
def touch(position2):
    if position2 == 'north':
        MoveArm1([16,0,0])  #elbow up
        print("Elbow Up")
```
```

![](bbox=[0.25, 0.59, 0.58, 0.76])

# 27 Add more touch movements

Now add some more movements to the program. On the next line down and indented inline with the `if` statement position, add an `elif` statement to check for the south position being touched, line 1. If you touch the board at the bottom, in the south position, then it will register the response and move the elbow down, line 2. Save your program by pressing F5, then run and test it.

```
```python
elif position2 == 'south':
    MoveArm1([32,0,0])  #elbow down
```
```

# 28 Add control for the grip

Continue to build up and assign the arm movements to the various gestures you make. Below the previous line of code add another `elif` statement to check for the west position, line 1, then use the arm command code to open the grip, line 2. Close the grip by touching east on the Skywriter, line three, and then add the code to close the grip, line 4.

```
```python
elif position2 == 'west':
    MoveArm1([1,0,0])  #grip close
elif position2 == 'east':
    MoveArm1([2,0,0])  #grip open
```
```

# 29 Using Taps

Any of the Skywriter gestures can be used to control the arm. On a new line, create a new function to identify taps, line 1. Note that the repeat rate is set to a value of 1 to remove the possibility of a double tap. Next create a new variable called position1, line 2. This is to stop the gesture overwriting the previous variable (For example, if the light is turned on, you might wish to move the arm but keep the light turned on). On line 4, check the position of the tap, then print the movement that the arm will make, line 5 (This is optional). As with the previous steps, assign the movement code for the arm; for example move the shoulder up, line 6.

```
```python
@skywriter.tap(repeat_rate=1)
def tap_tap(position1):
    print("Tap", position1)
    if position1 == 'north':
        print("Shoulder Up!")
        MoveArm1([64,0,0])  #shoulder up
```
```

# 30 Shoulder down

To move the shoulder down, use a similar format to that in Step 27. On the next line down, in line with the indentation level of the `if` statement, add an `elif` statement to check for a tap on the south position, line 1. Add an optional print statement to display that a tap has been registered, line 2, and then add the command to move the shoulder downwards, line 3. Save and run your program.

```
```python
elif position1 == 'south':
    print("Shoulder Down!")
    MoveArm1([128,0,0])  #shoulder down
```
```

# 31 Put it all together

Continue to create your program in a similar fashion as demonstrated in Steps 26 to 30. First choose the type of gesture/input that you want to use, then set up a function to identify the gesture and the position on the Skywriter where the gesture took place, for example, north, south, west etc. Next use conditional, `if` and `elif` statements, to check the position and then respond with a robot arm movement using the codes found in the full listing. Use the example program in the tutorial resources as a basic set up for your ideas and then expand and customise to add your own gestures and movements.