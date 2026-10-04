# ## 2.3 Zope Objects

Let's take a closer look at Zope's objectoriented approach as well as individual Zope objects such as DTML methods and documents, folders, external methods, and so on. As we do, you'll become familiar with each object's functions and their relationships to each other. Then we'll show you how to create your own objects; use them to perform various tasks; and how to copy, delete, and rename folders and other objects.

# ### 2.3.1 Zope and Object-Oriented Programming

Zope's most important underpinning is object-oriented programming.

> > NOTE You can skip this section and still get satisfactory results. However, to take full advantage of all Zope's benefits and gain a complete understanding of how it works, we strongly recommend that you read it.

The object-oriented philosophy is based on the fact that the world consists of discrete objects. An object is a real-world thing, with a status and the ability to perform actions and communicate with other objects. In a programming language, we can represent any individual real-world thing—be a house, a table, or a car—an object with properties.

For example, imagine a spaceship called the USS Chuck with a maximum crew of 120, 20 cargo bays, and a maximum speed of warp factor 9.6. The crew, the cargo, the speed, and the ship's name define the spaceship's state. But our spaceship must also perform actions, such as picking up crew, travelling through space, transporting freight, avoiding other spacecraft, and communicating with other spacecraft to perform avoidance maneuvers. How do we account for this information in a programming language?

# #### 2.3.1.1 Methods and Attributes

From a programming perspective

Because a spacecraft must be able to carry out certain functions, the appropriate methods must be implemented for it to function properly. We would write these methods or actions as pickCrewUp, fly, transportFreight, and avoidCraft. Together, the attributes and their values, as well as the implemented methods, define the spaceship object. An object is, therefore, defined by its attributes and methods.

An object is determined by what it knows and what it can do. For example, the USS Chuck knows how many crew members are on board, its speed, and how many of its cargo bays are full. In addition, it can carry out the actions specified by its methods.