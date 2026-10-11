
## Get started with Android Studio

Get your head around the early access preview of the next stage in Android development

Announced earlier this year at Google I/O, Android Studio will be the replacement for the current Android development solution in Eclipse. This Eclipse setup is part of the Android Developer Tools, and takes advantage of the IDE’s Java-based development environment and plug-in support to currently create the development portion of Android apps. With the rest of the SDK, virtual devices can be created and used to test code before deployment onto real devices.

The Android Studio aims to be an all-in-one solution for development and testing. Coming with the entire SDK, and not even requiring traditional compiling or installation on Linux, Android Studio is an incredibly easy and quick way to get straight into coding your apps – whether you’re an experienced Android/Java dev working directly in code, or a novice looking to use the graphical, drag-and-drop approach to app creation.

Android Studio is still currently in beta as a free early preview – we’ll cover some of the current quirks with the software. However, it’s definitely a great way to get used to using the software before the final switchover occurs. We’ll also cover how you can export from Eclipse if you’ve already been using that, and how to then distribute your app once it’s finally complete.

## Android Studio

Get to grips with the new IDE for Android development

![](img/dd9251551a61a36067892b1cc68615b0_24_0.png)

## Introducing Android Studio

The new Android Studio is based on IntelliJ IDEA, a much smaller and streamlined IDE than Eclipse. Android Studio utilises its features to create an all-in-one Android development environment with a smart visual view that is great for people just getting into app development, and the standard text editor for those who know their way around Java and the Android API.

Installation is very simple as well – the files contain both the IDE and the SDK you’ll need to create your apps, so you won’t need to install the SDK via ADT separately like you will have done with Eclipse if you’ve developed for Android in the past. The Studio allows you to edit how the SDKs are utilised, how imports and exports work, and even has a plug-in manager.

![](img/dd9251551a61a36067892b1cc68615b0_25_0.png)

- **Recent Projects**
  The recent projects view allows you to go straight into any project you wish to work on without having to look in the Open Project prompt

- **Check for updates**
  Android Studio has its own update manager, allowing you to keep it up to date. It will notify you when a newer version is available

- **New Project**
  Start a new project by going through the handy Android new project wizard, selecting API levels and setting the icon

- **Docs and How-Tos**
  Some tips and how-tos for IntelliJ, the base of Android Studio, are available straight from the welcome screen

### Installation

![](img/dd9251551a61a36067892b1cc68615b0_25_1.png)

**01 Download**
Head over to the Android Developers website and grab yourself a copy of the early access preview to Android Studio from here: **bit.ly/1bWFxz**
You’ll need to then extract the contents – put it in a folder you have easy access to, as you need to run the Studio from the folder.

![](img/dd9251551a61a36067892b1cc68615b0_25_2.png)

**02 Runtime**
Use `cd` in the terminal to navigate to the folder you just created, specifically the `android-studio/bin/` directory. To launch Android Studio, enter into the terminal: `$ ./studio.sh`
If it asks about your Java settings, for now press Enter, as we can fix that later if it becomes a problem.

![](img/dd9251551a61a36067892b1cc68615b0_25_3.png)

**03 First run**
If this is your first time using Android Studio, you can safely ignore the prompt to import any settings. Otherwise, find the file you created from before, or your old installation folder, to get previous settings. We can import from Eclipse later on.

## Android Studio

Get to grips with the new IDE for Android development

### Key features

### Development views

As the Java for the Android apps is split into visual and function elements, you can use a visual WYSIWYG editor for the XML code, allowing you to place buttons and text and other UI elements wherever you want on the screen. The text part is a full IDE, with code navigation, debugging, syntax highlighting and a smart code analyser that warns you of any obvious issues with what you've written.

![](img/dd9251551a61a36067892b1cc68615b0_26_0.png)

### Virtual devices

Test your apps on a virtual device that you define, either by using settings for the main Nexus devices, or by using generic settings for different-sized Android phones or tablets. You can edit the system settings to limit or increase RAM, and even allow it to use the system GPU if you need it to. It's not perfect, but it's a great way to quickly test functionality.

![](img/dd9251551a61a36067892b1cc68615b0_26_1.png)

### Eclipse migration

For existing Android developers, it's easy to migrate from Eclipse and the ADT to Android Studio. The tools are already in place to export the necessary files from Eclipse, and Android Studio includes a handy feature that allows you to then import them, and any other Studio file. This is helpful now and will be essential when it replaces Eclipse.

![](img/dd9251551a61a36067892b1cc68615b0_26_2.png)

### Debugging

A specific debugger can analyse the code as it runs and give you a full rundown of what's happening when, allowing you to go through the logs and figure out any possible issues, or work out where problems are already occurring. You can pause the program at any point to isolate issues, instead of having to search through code as it continues to run.

![](img/dd9251551a61a36067892b1cc68615b0_26_3.png)

### Helpful shortcuts

Android Studio has handy, configurable keyboard shortcuts. Here's a list of the most common to get you started...

| Action | Shortcut |
| :--- | :--- |
| Command look-up (autocomplete command name) | **Ctrl** + **Shift** + **A** |
| Project quick fix | **Alt** + **Enter** |
| Reformat code | **Ctrl** + **Alt** + **L** |
| Show docs for selected API | **Ctrl** + **Q** |
| Show parameters for selected method | **Ctrl** + **P** |
| Generate method | **Alt** + **Insert** |
| Navigate open tabs | **Alt** + **◄** / **Alt** + **►** |
| Jump to source | **F4** |
| Delete line | **Ctrl** + **Y** |
| Search by symbol name | **Ctrl** + **Alt** + **Shift** + **N** |
| Build | **Ctrl** + **F9** |
| Build and run | **Shift** + **F10** |
| Toggle project visibility | **Alt** + **1** |

## FAQ

Since Android Studio is still under some development, there are some bugs that still need to be ironed out. Here are a couple of known issues with Android Studio that you can work around.

**1) Error: Gradle project refresh failed**

Android Studio has a newer version of Gradle that has some backward compatibility issues. These can be fixed by first clicking the link to search build.gradle from the error dialog. From there, double-click the line under the build.gradle usage, opening the project build.gradle file. Edit the classpath to change the gradle version to '0.5.4.' Finally, save the file and rebuild your project.

**2) Error: Failed to import Gradle project**

This can be a problem after upgrading Android Studio, as the project file may point towards an SDK element that no longer exists. To fix this, you'll need to quickly install the Android Support Repository. First, open Android SDK Manager, find and expand Extras, and install Android Support Repository.

![](img/dd9251551a61a36067892b1cc68615b0_27_0.png)

## Migration

It's quite easy to export existing projects from Eclipse and then import them into Android Studio. First of all, make sure your ADT plug-in is up to date, then select File and Export. Open Android from there and select Generate Gradle Files, then your projects to export before clicking Finish. In the basic Android Studio window, click on 'Import project'. Find the build.gradle file and then press OK at the pop-up. You should then be able to start development on the project within Android Studio.

## Create a new project

**Android Studio offers a quick way to start your app**: name, package name, theme, advanced icon options and the ability to select between different Android APIs. The latter allows you to put together an app with specific versions of Android in mind, making newer API objects available for some. We'll look at a basic setup first so we can make our HelloWorld app later.

![](img/dd9251551a61a36067892b1cc68615b0_27_1.png)

### 01 Create New Project

From the Welcome screen, click on the Create New Project to open up the dialog window. Name the project HelloWorld – we'll be creating the code for that shortly. Leave all the other default settings – they relate to what versions of Android will be able to use the app.

![](img/dd9251551a61a36067892b1cc68615b0_27_2.png)

### 02 Set image

Here you can set your image, giving you a nice preview of how it will look on different types of devices. You can set padding, background colour and move to your app icon. For now, click Next, as we don't need an icon for the sample project.

![](img/dd9251551a61a36067892b1cc68615b0_27_3.png)

### 03 Activity selector

For now, we'll just use the blank activity. When making other apps, this activity selector can help you choose how the app will behave – such as being full-screen or having a multi-column flow to view several items.

![](img/dd9251551a61a36067892b1cc68615b0_27_4.png)

### 04 Activity name

Here you can name the activity and customise the way it works, with tabs, drop-down menus and other actions. For now, we'll leave this as is. Hit Finish and the project will be built. It may take a little while to do this.

![](img/dd9251551a61a36067892b1cc68615b0_27_5.png)

### 05 Project structure

Android Studio will create a lot of files for what will be a simple app – luckily we just need to pay attention to `MainActivity.java` and `MainActivity.xml` for the moment. The interface is also initially set up to allow for WYSIWYG visual development.

![](img/dd9251551a61a36067892b1cc68615b0_27_6.png)

### 06 Views

The default view is the visual development interface – it includes elements down the side that allow you to drag and drop functionality. You can also click the text tab to the bottom to get straight into the Java code, with a live preview updating as you type.
