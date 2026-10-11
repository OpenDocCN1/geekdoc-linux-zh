# PROGRAM A RASPBERRY PI QUADOPTER

**Propulsion** Here we're seeing the force from the propellers

**Vectors** Propeller force relative to Earth's axis (horizontal / vertical)

**Gravity** This term denotes the force of gravity

**Angle** This is the angle of tilt as defined by the quads sensors

![](bbox=[0.1, 0.22, 0.9, 0.6])

+   a_g = gravitational acceleration
+   a_q = quadcopter acceleration
+   a_qx } = a_q (reoriented to Earth's axes)
+   a_qy
+   ☐ = angle of tilt derived from accel + gyro

+   a_qx = tan ☐
+   a_qy for horizontal flight
+   a_qz = g => horizontal accel a_qx = g + a

# # Interpeter

The command interpreter converts a series of commands either from a radio control or programmed into the code itself. The commands combine the direction and speed compared to the horizon that the user want the quadcopter to follow. The code converts these commands into a series of targets for vertical speed, horizontal speed and yaw speed – any command from a pair of joysticks can be broken down into a set of these targets.

# # Inputs

The inputs to the quadcopter come from a series of electronic sensors providing information about its movement in the air. The main two are an accelerometer which measures acceleration force (including gravity) in the three axis of the quadcopter, and a gyroscope which measures the angular speed with which the quadcopter is pitching (nose/tail up and down), rolling (left/right side up and down), and yawing (spinning clockwise and anticlockwise around the central axis of the quadcopter itself).

# # Axes

The accelerometer is relative to the orientation of quadcopter axes, but the command targets are relative to the Earth's axes – the horizon and gravity. To convert the sensor output between the quadcopter axes and the Earth axes needs a little

# Understanding quadcopters...

Although this article focuses on software, a very basic background in the hardware from the kit is necessary to provide context.

A quadcopter has four propellers (hence the name) pointing upwards to the sky, each attached to its own brushless DC motor at one of the four corners of (usually) a square frame. Two motors spin clockwise, two anticlockwise, to minimise angular momentum of the quadcopter in flight.

Each motor is driven independently by an electronic speed controller (ESC). The motors themselves have three sets of coils (phases), and the ESCs convert a pulse-width-modulation (PWM) control signal from software/hardware to the three phase high-current output to drive the motors at a speed determined by the control signal.

The power for the ESCs and everything else on the system comes from a Lithium Polymer battery (LiPo) rated at 12v, 3300mA with peak surge current of 100A – herein lies the power!

> Above How sensors in the quadcopter point of view are converted to the Earth (horizontal / vertical) viewpoint to provide horizontal motion