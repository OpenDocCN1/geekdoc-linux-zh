![](bbox=[0.2, 0.12, 0.6, 0.55])

Figure 9-16: Camera Activation Box configured to set the camera to CamShot01 whenever the player is inside of it.

11. Also set this object to have a low opacity via the materials editor. Another good trick is to hide the room and camera act box to make it easier to see the objects inside of the room: click on the display tab (looks like a monitor), select the room object, click hide selected, select the camera act box, click hide selected.

12. Finally, we need to create a few objects which must exist somewhere in the level. (Their actual position is unimportant, as is their size; they hold data that the game engine will need when you run the level.) Create a small box somewhere in the Room, name it Camera01, and assign it the Camera class. Create another one named Levelobj and assign it the LevelObj class. Create a third called Matte01 and assign it the Matte class.