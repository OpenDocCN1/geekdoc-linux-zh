You can use anything that is translucent as a diffuser. Our favorite is a very thin styrene sheet — about 0.5mm thickness is fine and easy to work with, because it can be cut with scissors. (A good alternative is a simple sheet of paper.) If you have several LEDs and want to see the light from each individually, then you have to have each one surrounded by a light baffle — sometimes loosely in an egg box, or waffle box. Without the baffle, the light from each LED mixes with adjacent to it and gives a soft effect that is not at all unpleasant. The degree of diffusion you get is proportional to not only the diffusing material but also the distance of material from the LED. In many cases, a few millimeters is fine.

You can turn the clear-plastic housing LED into a diffuser by rubbing it with very fine sandpaper or wire wool. Even better is to use a foam-backed sanding block, because it rounds the curves better than paper. These LED housings are made of resin, so solvents like acetone do not affect the surface.

![](bbox=[0.175, 0.00242, 0.223, 0.00335])

# # Making more colors

The trick to making more colors than the primary and secondary colors is to have different brightness of each of the three colors. In that way, many more subtle colors can be. So how can you control the brightness of an LED? Well, the answer might not be immediately apparent, but what you need to do is to turn the LED on and off very rapidly. If you do this fast enough — that is, faster than 30 times a second — then the eye/brain sees this as a light that is constant and not flickering. Furthermore, you perceive the brightness of the LED according to the relative length of the On and Off times. That is, if the LED is on and off for equal times, the LED appears to be only half as bright. This rapid switching technique is known as PWM — short for Pulse-Width Modulation and is the way you control the LED’s brightness. The waveforms are shown in Figure 17-3.

| | Bright |
|---|---|
| On |
| Off |
| On | Medium |
| Off |
| On | Dim |


FIGURE 17-3: A PWM signal controlling the LED's brightness.

360 PART 5 Exploring Electronics with the Raspberry Pi