
![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_44_0.png)

Figure 9. The initial Fedora Core boot screen.

Step 1a. The system will wait for you to either press the Enter key if you want to run the installation in graphical mode, or to type in a command at the boot prompt if you need to do so. Some machines are persnickety when it comes to installing Linux (or maybe it’s the other way around), and so require the installation to be run with one or more parameters. This is where you would enter those parameters. Once the installation process begins, you’ll see a blank screen, as shown in Figure 10.

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_44_1.png)

Figure 10. Booting takes a few seconds, during which a blank, character-based screen appears.

**Step 1b.** After a few seconds more, a character-based dialog asks if you want to test the CD media before installing (see Figure 11). The character-based Media Check dialogs aren't mouse-enabled, so you'll need to use the left and right arrow and the Enter keys on your keyboard to select choices.

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_45_0.png)

**Figure 11.** *The CD Found dialog allows you to decide whether you want to check the CDs for errors before installation.*

**Step 2.** If you select OK, continue reading at step 3. Otherwise, skip to step 5. (Hint: You should do the CD test at least once. It is possible that a bad CD will pass this test, but you can cut down the odds of wasting time with a bad CD if you test it.)

**Step 3.** You'll get a second dialog, as shown in Figure 12, that offers two choices: one to test the CD currently in the drive, and another to eject the current CD and insert a different one to be tested.

**Step 3a.** Whether you elect to test the current CD or eject the CD and insert another, you'll soon enough be greeted by the Checking dialog, as shown in Figure 13.

**Step 3b.** Once the media check is complete, the thermometer bar will sit at 100% for another 15–30 seconds, as shown in Figure 14.

**Step 3d.** The Media Check dialog will display the results of testing the CD in the drive, as shown in Figure 15.

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_46_0.png)

**Figure 12.** The second Media Check dialog offers choices to test the current CD or insert a different CD.

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_46_1.png)

**Figure 13.** The Checking dialog of the Media Check process displays the progress with a thermometer bar.

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_47_0.png)

Figure 14. The thermometer bar will sit at 100% for a short period of time.

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_47_1.png)

Figure 15. The results of the media check are displayed in a separate dialog.

Step 4. Click OK. You’ll get a chance to test another CD or to continue with the installation process, as shown in **Figure 16**. Selecting *Test* will cycle through step 3 again, while selecting *Continue* will continue the installation process, as described in step 5.

Step 5. After selecting *Skip* in step 1b or *Continue* in step 5, the character-based screen will scroll off the display as feedback about the installation process starts to appear, as shown in **Figures 17** and **18**.

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_48_0.png)

**Figure 16.** The Media Check process allows you to test additional CDs or continue with installation.

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_48_1.png)

**Figure 17.** Feedback about installation begins with a “Running anaconda” line.

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_49_0.png)

**Figure 18.** Feedback continues with lines about probing for devices.

After 30 to 60 seconds, a graphical X appears on the screen, followed by the Fedora Core logo as shown in **Figure 19**. This means that the graphical subsystem has kicked in, and the rest of the installation will be done graphically, and (hopefully) with mouse support. (If your mouse doesn’t work, you can manage to get through the GUI with the keyboard, so you can try to select a different mouse during the installation procedure.)

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_49_1.png)

**Figure 19.** The appearance of the Fedora Core logo means that the graphical part of installation has begun.

## Perform installation

The Welcome screen appears to start off the installation wizard. It consists of a two-pane dialog. Help text is in the left pane, and tasks to perform are displayed in the right pane, as shown in Figure 20.

### Welcome screen

**Step 6.** Click Next to open the first installation screen, Language Selection, as shown in **Figure 21**—after carefully reading every word of the Welcome text in the left pane, of course.

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_50_0.png)

**Figure 20.** The “Welcome to Fedora Core” screen starts the installation wizard.

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_50_1.png)

**Figure 21.** The Language Selection screen controls the installation process.

### Language Selection

**Step 7.** Choose the language you want to use during installation, and then click **Next** to open the **Keyboard Configuration** screen, as shown in **Figure 22**.

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_51_0.png)

**Figure 22.** The **Keyboard Configuration** screen.

### Keyboard Configuration

**Step 8.** Choose the keyboard layout you want to use on your system, and then click **Next** to open the **Mouse Configuration** screen, as shown in **Figure 23**.

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_51_1.png)

**Figure 23.** The **Mouse Configuration** screen.

### Mouse Configuration

Step 9. Select your mouse. Mine was detected as a Generic 3 Button Mouse (USB) and I changed it to the right one—a Microsoft IntelliMouse Optical (USB). You may have to experiment a bit if you're using offbeat hardware. If your mouse has only two buttons, select the “Emulate 3 buttons” check box. Doing so enables you to click both buttons at the same time to take the place of clicking the middle button.

Then click Next to open the Monitor Configuration screen, as shown in Figure 24.

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_52_0.png)

Figure 24. The Monitor Configuration screen.

### Monitor Configuration

Step 10. Again, depending on your hardware, your monitor may already have been detected and shown as selected in the screen. If not, you can either choose “Generic monitor” at the very top of the list, manually choose your monitor if it's in the list, or choose the closest available choice to your monitor from the list. Then click Next to bring forward the Installation Type dialog, as shown in Figure 25.

### Installation Type

The Fedora Core distribution comes with literally hundreds of software packages in addition to the basic Linux operating system. The three FC CDs also include Office suites, Web browsers, e-mail clients, drawing packages, PDF viewers, and utilities, as well as tools for administration, programming, and a variety of servers (such as e-mail servers, network file servers, and Web servers). These packages, in toto, represent functionality for a wide variety of users, from power users to programmers to server administrators. Not everyone would use all of these packages. Instead, each type of user would use a subset of packages.

As a result, most users will not install every single package, although that could be done if a user wanted to use a machine for a wide variety of purposes (not advisable unless you know what you're doing). Instead, most users will want to select a subset of packages that would be used for a particular purpose. Installing packages that you have no use for could open your system to security vulnerabilities. Later, if you find a package that you want but didn't install, you can always install it then.

Because there are so many packages, it would be awkward, if not impossible, for most users to identify and install just the packages they want. Fedora Core comes with three predefined configurations of packages—one for power users (called “Desktop”), one for programmers (called “Workstation”), and one for server administrators (called “Server”). In addition, a fourth configuration allows users to customize their choices, but because you can customize the first three configurations too, it’s not really necessary.

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_53_0.png)

Figure 25. The Installation Type dialog.

Step 11. Select the “Personal Desktop” option, because you’re installing for an end-user machine. Then click Next to open the Disk Partitioning Setup screen, as shown in Figure 26.

### Disk Partitioning Setup

The Fedora Core installation wizard provides a number of options for partitioning your hard disk. (See Appendix A, “Partitions,” for a detailed explanation of how partitions work with respect to Linux.) According to the Disk Partitioning Setup screen, you can have FC automatically create partitions or you can manually partition the hard disk yourself by using FC’s Disk Druid tool. If you choose automatic partitioning, FC will create several partitions by default that are good enough for many users. If you choose manual partitioning, you’ll have to create every partition yourself. With automatic partitioning, you’ll be able to review and modify the default partitions through Disk Druid, so there’s no real advantage to selecting manual partitioning.

Step 12. Select “Automatically partition” and click the Next button to open the Automatic Partitioning screen, as shown in Figure 27.
