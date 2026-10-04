
![](img/43a28cce5475b2f487bf455365567fb6_37_0.png)

Figure 2-4: The management screen with left and right frames.

## 2.2.1 The Left Frame of the Management Screen

The left frame of the management screen (Figure 2-5) shows a hierarchical view of all folders and other container objects on the Zope server (section 2.3). To quickly navigate through them, click a folder to list its objects in the right-hand frame. Click the plus and minus icons next to the folders in the left frame to expand or collapse the view of the object hierarchy.

![](img/43a28cce5475b2f487bf455365567fb6_37_1.png)

Figure 2-5: The left frame of the management screen (current user information appears in the tab frame by default).

- The Zope Corporation link takes you to the Zope copyright page, Zope Python licenses, and the Zope credits.
- Click Refresh at any time to update the left frame; this function is particularly useful if you've been working on the server for a while and have created or deleted objects.
- The name of the Zope server user, User1, appears at the bottom of the left frame.

## 2.2.2 The Right Frame of the Management Screen

The tabs at the top of the right frame of the management window (Figure 2-6) give you access to the various management pages or views of the currently selected object. For example, here you can edit the object's contents or properties, locate other objects with Find, or even undo certain actions (Chapter 3).

![](img/43a28cce5475b2f487bf455365567fb6_38_0.png)

Figure 2-6: The right frame of the management window

- The complete path for the object you are working on directly beneath the tab bar. Click the links in the path to move up the folder hierarchy.
- The Add Objects menu, found only on the Contents View tab, lets you create various Zope objects.
- Help buttons within views link to help text, which contains additional information related to the functions in the current view.

## 2.3 Zope Objects

Let's take a closer look at Zope's object-oriented approach as well as individual Zope objects such as DTML methods and documents, folders, external methods, and so on. As we do, you'll become familiar with each object's functions and their relationships to each other. Then we'll show you how to create your own objects; use them to perform various tasks; and how to copy, delete, and rename folders and other objects.

### 2.3.1 Zope and Object-Oriented Programming

Zope's most important underpinning is object-oriented programming.

> NOTE You can skip this section and still get satisfactory results. However, to take full advantage of all Zope's benefits and gain a complete understanding of how it works, we strongly recommend that you read it.

The object-oriented philosophy is based on the fact that the world consists of discrete objects. An object is a real-world thing, with a status and the ability to perform actions and communicate with other objects. In a programming language, we can represent any individual real-world thing—a house, a table, or a car—an object with properties.

For example, imagine a spaceship called the USS Chuck with a maximum crew of 120, 20 cargo bays, and a maximum speed of warp factor 9.6. The crew, the cargo, the speed, and the ship's name define the spaceship's state. But our spaceship must also perform actions, such as picking up crew, travelling through space, transporting freight, avoiding other spacecraft, and communicating with other spacecraft to perform avoidance maneuvers. How do we account for this information in a programming language?

#### 2.3.1.1 Methods and Attributes

From a programming perspective

Because a spacecraft must be able to carry out certain functions, the appropriate methods must be implemented for it to function properly. We would write these methods or actions as pickCrewUp, fly, transportFreight, and avoidCraft. Together, the attributes and their values, as well as the implemented methods, define the spaceship object. An object is, therefore, defined by its attributes and methods.

An object is determined by what it knows and what it can do. For example, the USS Chuck knows how many crew members are on board, its speed, and how many of its cargo bays are full. In addition, it can carry out the actions specified by its methods.

#### 2.3.1.2 Classes

Now imagine that the USS Chuck meets a similar spaceship, the USS Largo. The Largo is smaller, fewer crew members, and its maximum speed is less than the USS Chuck's. The ships communicate with each other, and the smaller ship begins an evasive maneuver.

Despite the differences between the two crafts, both are spaceships with identical capabilities, such as the ability to perform evasive maneuvers, pick up crew, and so on; they differ in their characteristics, namely size and maximum speed. You would have to check the attributes and implemented methods of the USS Largo, you would find that, from the specific attribute values, they match those of the USS Chuck. Because the objects can carry out the same actions, they do belong to the same class. A class describes all objects that have the same methods and attributes.

### 2.3.1.3 Objects

A folder is a container that can hold other objects, including other folders. This allows for a hierarchical structure of objects. Each object in Zope has an ID, which is a unique identifier within its folder. Objects also have attributes, which are properties that describe the object, and methods, which are actions that the object can perform.

There are many types of objects in Zope, including:

- Folders: Containers used to organize other objects.
- Files: Objects that store data, such as text, images, or documents.
- Methods: Objects that perform actions.
- External Methods: Methods that are implemented in other languages, such as Python or C++.
- Templates: Objects that are used to generate HTML or other dynamic content.

### 2.3.2 Creating a Folder

To create a folder in Zope, you can use the management interface. Navigate to the folder where you want to create the new folder, click the Add Objects menu, and select Folder. In the configuration form, enter the ID and title for the folder. You can also select options to create a public interface or a user folder.

| Field | Value |
| :--- | :--- |
| Id | Image_archive |
| Title | |
| Create public interface | [ ] |
| Create user folder | [ ] |

Figure 2-7: Creating a folder

#### 2.3.1 Example: Creating an Image Archive

To create an image archive, you create an empty folder for storing image files as follows:

- Create a folder with the id Image_archive in the Zope root folder by opening the Add Objects menu and selecting Folder (Figure 2-8), then entering the appropriate information on the configuration form. Leave the check boxes blank.
