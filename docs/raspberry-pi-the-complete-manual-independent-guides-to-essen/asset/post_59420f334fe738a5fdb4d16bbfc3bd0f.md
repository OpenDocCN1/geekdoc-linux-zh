
# Program a quadcopter

## Projects

### What you'll need...

- Raspijan
  www.raspberrypi.org/downloads
- Python
  www.python.org/doc

# Program a quadcopter

How do you push the limits of the Pi? You give it wings. Andy Baker shows us how it's done...

The Raspberry Pi is a fantastic project board. Since we love a challenge, we set out looking for something that would really push the limits of our hacking and coding skills. We chose a quadcopter.

This article uses the Python code available online as a guide through what's needed to build a quadcopter, metaphorically bolting it together so that by the end you don't just understand the code but also the interaction with the real-world to enable you to build your own quadcopter with confidence. You can find Andy's code on his blog.

# Did you know...

> Andy Baker, the writer of this article, keeps a blog at blog.pistuffing.co.uk that's a great insight into his project

![](img/59caadfa348382a5c408c25137901e27_137_0.png)

**Right** Put your Raspberry Pi in the sky with our expert coding guide!

## Sensor viewpoint diagram

How sensors in the quadcopter's point of view are converted to the Earth (horizontal/vertical) viewpoint to provide horizontal motion

![](img/59caadfa348382a5c408c25137901e27_138_0.png)

# Interpreter

**01** The command interpreter converts a series of commands either from a radio control or programmed into the code itself. The commands combine the direction and speed compared to the horizon that the user wants the quadcopter to follow. The code converts these commands into a series of targets for vertical speed, horizontal speed and yaw speed – any command from a pair of joysticks can be broken down into a set of these targets.

# Inputs

**02** The inputs to the quadcopter come from a series of electronic sensors providing information about its movement in the air. The main two are an accelerometer which measures acceleration force (including gravity) in the three axes of the quadcopter, and a gyroscope which measures the angular speed with which the quadcopter is pitching (nose/tail up and down), rolling (left/right side up and down), and yawing (spinning clockwise and anticlockwise around the central axis of the quadcopter itself).

# Axes

**03** The accelerometer is relative to the orientation of quadcopter axes, but the command targets are relative to the Earth's axes – the horizon and gravity. To convert the sensor output between the quadcopter axes and the Earth axes requires the use of a lot of mathematics, specifically trigonometry. You also need knowledge of the tilt angles in pitch and roll axes of the quadcopter with respect to the Earth. It's pretty complicated stuff, but the diagrams on these pages should help you understand the logic.

![](img/59caadfa348382a5c408c25137901e27_139_0.png)

*Above* Kits are available as ready to fly (RTF) if you just want the joy of flight, but where's the challenge in that? We started with a almost-ready to fly (ARTF) kit - the DJI Flame Wheel F450 - all the hardware, but none of the control electronics or software. Many enthusiasts have created DIY quadcopter using Arduino microcontrollers, so we knew a DIY build was possible, but very fussy, if any, have successfully used the Raspberry Pi.

# Angles

**04** Both the accelerometer and gyro can provide this angle information, but both have flaws. The accelerometer output can be used to calculate the angle by using the Euler algorithm. However, the accelerometer output is plagued by noise from the motors/propellers, meaning a single reading can be hugely inaccurate; on the plus side, the average reading remains accurate over time.

In contrast, the gyro output does not suffer from the noise, but since it is the angular speed being measured, it needs to be integrated over time to find the absolute angle of the quadcopter in comparison to the horizon. Rounding errors in the integration lead to ever increasing errors over time, ultimately curtailing the maximum length of a flight.

# Filter

**05** They are both flawed, they can be merged mathematically such that each compensates for the flaws in the other, resulting in a noise-free, long-term accurate reading. There are many versions of these mathematical noise/drift filters. The best common one is by Kalman; the one we've chosen is slightly less accurate, but easier to understand and therefore to code: the complementary filter.

Now with an accurate angle in hand, it's possible to convert accelerometer sensor data to inputs relative to the Earth's axes and work out how fast the quadcopter is moving up, down, left, right and forwards and backwards compared to the targets that have been set.

![](img/59caadfa348382a5c408c25137901e27_139_1.png)

# PIDs

**06** So we now have a target for what we want the quadcopter to do, and an input for what it’s doing, and some motors to close the gap between the two; all we need now is a way to join these together. A direct mathematical algorithm is high on impossible – accurate weight of the quadcopter, power per rotation of each blade, weight imbalance etc. would need to be incorporated into the equation. And yet none of these factors is stable during flight (and cached), blades get damaged, batteries move in the frame, grass/mud/moisture changes the weight of the copter, humidity and altitude would need to be accounted for. Hopefully it’s clear this approach simply won’t fly.

Instead, an estimation method is used with feedback from the sensors to fine-tune that estimate. Because the estimation/feedback code loop spins at over 100 times a second, this approach can react to ‘errors’ very quickly, indeed, and yet it knows nothing about all the factors which it is compensating for – that’s all handled blindly by the feedback, this is the PID algorithm. It takes the target, subtracts the feedback input, resulting in the error. The error is then processed via a Proportional, Integral and a Differential algorithm to produce the output.

# Blender

**07** The outputs are applied to each ESC in turn; the vertical speed output is applied equally to all blades, the pitch rate output is split 50/50 subtracting from the front blades and adding to the back, producing the pitch. Roll is handled similarly. Now yaw is handled in a similar way, but applied to diagonal blades which spin in the same direction.

These ESC-specific outputs are then converted to a PWM signal to feed to the hardware ESCs with the updated propeller/motor speeds.

![](img/59caadfa348382a5c408c25137901e27_140_0.png)

# Quadcopter orientation

The orientation of the quadcopter compared to the direction of travel, the rotation of the propellers and the axes used in the code

# Understanding quadcopters…

Although this article focuses on software, a very basic background into the hardware from the kit is necessary to provide context.

A quadcopter has four propellers (hence the name) pointing upwards to the sky, each attached to its own brushless DC motor at one of the four corners of usually a square frame. Two motors spin clockwise, two anti-clockwise, to minimise angular momentum of the quadcopter in flight.

Each motor is driven independently by an electronic speed controller (ESC). The motors themselves have three sets of coils (phases), and the ESCs convert a pulse-width-modulation (PWM) control signal from software (hardware to the three phase) high-current output to drive the motors as a speed determined by the control signal.

The power for the ESCs and everything else on the system comes from a Lithium Polymer battery (LiPo) rated at 250~3300mA with peak surge current of 100A. It’s hairless less the power!

# Sensors

The quadcopter’s sensors report data according to these x, y and z axes

# Orientation

The overall orientation of the quadcopter depicting front, back, left and right relative to the sensor and propeller layouts

# Code and reality

![](img/59caadfa348382a5c408c25137901e27_141_0.png)

In this code, there are nine PIDs in total. In the horizontal plane, for both the X- and Y axes, the angle desired PIDs convert the user-defined desired tilt target to the angle desired and angle of tilt target, the angles required to convert this desired tilt angle to the desired tilt rate. The rotation speed PID then converts the desired tilt rate to a motor speed, which in the vertical direction, a single PID converts the desired rate of yaw to a motor speed. Finally, prevention of yaw (like a spinning top) uses two PIDs - one to set the desired spin rate, one to keep rotation steady. The output of the nine PIDs can be compared to the front and back propellers. While some PIDs are independent, others interact with each other. For example, the X-axis PID interacts with the Y-axis PID, and the tilt PID interacts with the heading PID. This means that changing one PID can affect the others.

Headwind will drift backwards. A tailwind will drift forwards. Crosswind will drift sideways. These drifts are caused by the horizontal thrust of the propellers. When the copter is accelerating, it pitches forward or backward to generate the required thrust. This causes a horizontal force that moves the copter in the direction of the wind. To counteract this, the flight controller can use the vertical PIDs to adjust the copter's attitude and reduce the drift.

> Taking the drift suppression first, a quadcopter in a headwind will drift backwards due to the force applied by the wind

The most critical part of the PID tuning is the heading PID. This PID is responsible for keeping the copter pointing in the desired direction. If the heading PID is not tuned correctly, the copter will oscillate or drift. The heading PID is also affected by the wind. A strong headwind will cause the copter to yaw backwards, while a tailwind will cause it to yaw forwards. The crosswind will cause the copter to yaw sideways. To counteract these effects, the heading PID can be adjusted to compensate for the wind.
