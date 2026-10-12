# Projects

# Program a quadcopter

# Code and reality

![](bbox=[0.08, 0.19, 0.16, 0.31])

In this code, there are nine PIDs in total. In the horizontal plane, for both the X- and Y axes, the angle desired PIDs convert the user-defined desired tilt target to the angle desired and angle of tilt target, the angles required to convert this desired tilt angle to the desired tilt rate. The rotation speed PID then converts the desired tilt rate to a motor speed, which in the vertical direction, a single PID converts the desired rate of yaw to a motor speed. Finally, prevention of yaw (like a spinning top) uses two PIDs - one to set the desired spin rate, one to keep rotation steady. The output of the nine PIDs can be compared to the front and back propellers. While some PIDs are independent, others interact with each other. For example, the X-axis PID interacts with the Y-axis PID, and the tilt PID interacts with the heading PID. This means that changing one PID can affect the others.

Headwind will drift backwards. A tailwind will drift forwards. Crosswind will drift sideways. These drifts are caused by the horizontal thrust of the propellers. When the copter is accelerating, it pitches forward or backward to generate the required thrust. This causes a horizontal force that moves the copter in the direction of the wind. To counteract this, the flight controller can use the vertical PIDs to adjust the copter's attitude and reduce the drift.

> Taking the drift suppression first, a quadcopter in a headwind will drift backwards due to the force applied by the wind

The most critical part of the PID tuning is the heading PID. This PID is responsible for keeping the copter pointing in the desired direction. If the heading PID is not tuned correctly, the copter will oscillate or drift. The heading PID is also affected by the wind. A strong headwind will cause the copter to yaw backwards, while a tailwind will cause it to yaw forwards. The crosswind will cause the copter to yaw sideways. To counteract these effects, the heading PID can be adjusted to compensate for the wind.