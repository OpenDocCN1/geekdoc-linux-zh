# Chapter 9: What Lies Ahead?

![](bbox=[0.15, 0.1, 0.68, 0.55])

Figure 9.15: Camshot with target and tracking fields set up. On your screen the purple object is the Camshot, the red object is the target, and the blue object is the player.

+   10. Camera shots are activated by a special kind of Activation Box object, called an ActboxOR (short for Activation Box with Object Reference). Create a box that encloses the floor and player objects, but is itself contained by the Room box. Name it Cambox01 and assign it the ActboxOR class. We want this activation box to activate Camshot01 any time that Player01 is inside of Cambox01, so set ActBox01,—Mailbox to 1021 (the mailbox to write CamShot references to; see reference manual for details), Object to CamShot01, Activated By To Actor, and Actor to Player01.