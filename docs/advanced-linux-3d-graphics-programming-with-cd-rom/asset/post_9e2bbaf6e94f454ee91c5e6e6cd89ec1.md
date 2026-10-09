
## Chapter 9
## What Lies Ahead?

This chapter aims to give you a glance at some exciting trends affecting Linux 3D graphics programming. We begin by looking at two *content development systems* currently available for Linux. We then make some speculations about future directions of 3D graphics. Finally, we review the contents of this book within the context of 3D graphics programming in general.

### Content Development Systems

In this section, we'll take a brief look at two 3D content development systems. Here, the term *3D content development system* refers to a visual 3D environment that allows the creation of interactive content with a minimum of programming. Such systems show us the direction that future 3D development might take.

### Game Blender/Blender 2.0

Blender 2.0, also called Game Blender, is a version of Blender that includes some support for creating interactive content. We don't have the space in this book to go over the complete details of the entire system. What we can do is go over a quick example of how to create a simple game in Blender, so that you can see how the system works and experiment further on your own.

> **NOTE** To execute the following tutorial, you must download the Game Blender system (version 2.0 or higher) from the Blender home page, <http://www.blender.nl>. The program is free of charge.

The following tutorial shows you how to create a simple world in Blender and navigate through it in real time.

- 1. Start Blender and clear the screen by pressing **Ctrl+x, Enter**. Select and delete the default plane object. Ensure you are in top view: press 7 on the numeric keypad.
- 2. Add a large cube object by selecting **Add, Mesh, Cube** from the Toolbox (press **Space**). Scale the cube so that it is approximately 15 units long on each side. Exit EditMode.

![](img/a19d4e8b1d7eb6387691dc6c865430e6_600_0.png)

- 3. Change to the RealtimeButtons by pressing **F8**. Click the **Sector** button in the upper left of the ButtonsWindow. This sets the large cube mesh to be a sector.

> **NOTE** Starting with version 2.11, Blender has done away with explicit marking of sectors, so you do not need to execute the previous step with Blender 2.11 or higher.

- 4. In the 3DWindow, add an Isosphere by selecting **Add, Mesh, Isosphere** from the Toolbox. Select subdivision **2**, and press **Enter**. Drag the topmost vertex of the sphere slightly forward, so that the sphere has a discernible tip. Exit EditMode. Ensure the sphere is still selected.

![](img/a19d4e8b1d7eb6387691dc6c865430e6_600_1.png)

- 5. In the RealtimeButtons, click the **Actor** button to flag the sphere as an actor. Then click the **MainActor** button, which marks the sphere as the main actor in the game. Also click the **Dynamic** button, which allows the object to be controlled by the Blender dynamics system.

> Blender 2.11 has a new interface for the rigid body dynamics subsystem. There is no MainActor button. Also, click the RigidBody button to allow the sphere to be controlled as a rigid body by the physics subsystem.

- 6. Move the cursor into the ButtonsWindow and maximize it by pressing Ctrl+Down Arrow. We are now going to program in the keyboard handler so that we can move the sphere around with the keyboard. Doing this requires us to create sensors, controllers, and actuators.
- 7. In the Sensors column click the **Add** button four times. Do the same in the Controllers and Actuators columns. This creates four sensors, four controllers, and four actuators. We are going to have four keys which we use to control the sphere, and thus, four objects of each type.

![](img/a19d4e8b1d7eb6387691dc6c865430e6_601_0.png)

- 8. Notice the small pebble to the right of each sensor, and the small hole to the left of each controller. Left-click the pebble and drag it into the hole, creating a link between sensor and controller. Do this for all controllers. Also repeat the procedure with the controllers and the actuators.

![](img/a19d4e8b1d7eb6387691dc6c865430e6_602_0.png)

- 9. Notice that each sensor contains a pop-up menu field with the value “Always.” Change each of these fields to contain the value “Keyboard”. Click on each field, notice the menu which appears, and select **Keyboard**.

![](img/a19d4e8b1d7eb6387691dc6c865430e6_602_1.png)

- 10. Assign each keyboard sensor a different key as follows. Click on the Key field for the first sensor. Notice the message “Press any key.” Press **Left Arrow**. Notice that “Leftarrow” appears in the field. Do the same for the remaining three sensors, with keys **Right Arrow**, **Up Arrow**, and **Down Arrow**.

![](img/a19d4e8b1d7eb6387691dc6c865430e6_603_0.png)

- 11. Change the actuators to respond to the keys as follows. For the first actuator, type **1.00** in the third torque field. For the second actuator, type **-1.00** in the third torque field. For the third actuator, type **1.00** in the second force field. For the fourth actuator, type **-1.00** in the second force field. The fields in the actuators allow you to apply forces and torques to the object whenever the sensor fires. The three fields represent $x$, $y$, and $z$ components of the applied force.

![](img/a19d4e8b1d7eb6387691dc6c865430e6_603_1.png)

- 12. Restore the ButtonsWindow to its original size by pressing Ctrl+Down Arrow.
- 13. In the 3DWindow, add another cube object, slightly smaller than the original cube. Flip all vertex normals to point inside by typing a until all vertices are selected (yellow), then press Ctrl+Shift+n and press Enter to flip the normals. Exit EditMode. Ensure the cube object is still selected.

![](img/a19d4e8b1d7eb6387691dc6c865430e6_604_0.png)

- 14. Move the mouse cursor over the ButtonsWindow, and press Home. This ensures that all buttons are visible. Then, click the button Prop. This marks the smaller cube as an object within the larger sector.

> **NOTE** Blender 2.11 has eliminated the Prop button; props do not need to be explicitly marked.

- 15. In the 3DWindow, select the camera object by right-clicking. In the RealtimeButtons, click Actor: Add a sensor, controller, and actuator, and link them together. Leave the sensor type with its default value “Always.”
- 16. Change the actuator to be of type “Camera”: Click on the pop-up menu that reads “Object,” and notice the menu which appears. Select Camera. This type of actuator causes the camera to follow a target object.
- 17. In the actuator field OB., type Sphere. This is the name of the Icosphere object we added earlier, and is the object that the camera will track. In field Height., type 5.00. In field Min., type 5.00. In field Max., type 10.00. These set the constraints on the camera position with respect to the target object.

![](img/a19d4e8b1d7eb6387691dc6c865430e6_605_0.png)

- 18. In the 3D Window, switch to camera view by pressing **0** on the numeric keypad. Press **Shift+p** to start playing the game.
- 19. Press the arrow keys to move the sphere through the environment. Notice that the camera tracks the object automatically, that you cannot move through the walls or floor of the environment, and that gravity forces are applied. Press **Esc** to end the simulation.

![](img/a19d4e8b1d7eb6387691dc6c865430e6_605_1.png)

> **NOTE** In Blender 2.11 the sphere will bounce up and down upon hitting the ground, because of the default collision handling parameters. You can correct this by explicitly specifying the material properties of the sphere and/or the surrounding cube through the MaterialButtons.

> **TIP** You can also run the simulation from any other viewpoint, not just camera view. For instance, top view is useful for getting a bird's-eye picture of the environment.

A few notes on the system are in order:

- You can run the game in textured mode (press Alt+H2), but this requires a hardware accelerator for acceptable performance.
- Python scripting support is planned to allow for game logic to be coded in the Python language. Preliminary support already exists.
- The visibility scheme is apparently a modified portal scheme where the portals are the faces of the bounding boxes, as discussed in Chapter 8.

This simple example gives you an idea of how the Game Blender system works. The system is very visual, using links connected via drag-and-drop in the RealtimelButtons. A system that achieves similar goals but which takes a different approach is offered by World Foundry, which we look at next.

### World Foundry

World Foundry is an open source (GPL) package that enables non-programmers to create 3D environments and games. It combines a powerful 3D engine with an external level editing system and an internal scripting system.

> **NOTE** The World Foundry project (http://www.worldfoundry.org) currently needs interested 3D programmers to assist in porting and extending the engine and tools. You—yes, you!—can help in this process. World Foundry is an extremely powerful system; I have not seen any other open source projects which rival it. Furthermore, World Foundry is cross platform, meaning that games can be developed for Linux and Windows.

The Blender system for assigning behaviors to objects involved visually dragging links to connect sensors, controllers, and actuators. In contrast to this, the World Foundry approach uses scripts to control behavior. The scripting language is a dialect of Scheme, which is a variant of LISP. World Foundry provides a number of example scripts for common behaviors. Creation and placement of geometry in 3D space within World Foundry is still done visually, in a 3D level editing program. (Indeed, I am attempting to adapt Blender to be used for exactly this purpose.)

One can argue whether scripting or a visual system is more flexible. My personal opinion as a programmer is that for real reuse and modularity with complex structures, there is no substitute for using a programming language. Formal languages allow us to express and manage complexity in a precise way. Visual development tools usually are good for rapid development, but are poor when it comes to reusable structure. It could be argued, however, that the types of structures created with a visual system are inherently simple, because the underlying system hides the complexity. You’ll have to decide for yourself which system best suits your needs, your style, and your project. It
