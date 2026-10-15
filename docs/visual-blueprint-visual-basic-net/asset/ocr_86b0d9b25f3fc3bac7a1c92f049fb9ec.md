# Extra

The type of events you use can create more or less interaction, depending on what is necessary for your application. Small but useful interactions can include changing labels or colors in the control as the user moves their mouse around. Most visual controls provide MouseEnter, MouseLeave, and MouseHover events. These events fire when the mouse enters the control, leaves the control, and stays on top of the control for a few moments, respectively.

Not all events are in response to user interaction. All visual controls and the form itself have a Paint event. In this event, you provide code to draw directly onto the surface of the control. For example, you can draw a pattern in the background of a button. This event triggers anytime all or part of the control or form invalidates. Invalidation is when some part of the control or form needs to redraw. You can force a control or form to invalidate by using the Invalidate method of the component.

![](bbox=[0.06, 0.48, 0.52, 0.78])

![](bbox=[0.52, 0.48, 0.95, 0.78])