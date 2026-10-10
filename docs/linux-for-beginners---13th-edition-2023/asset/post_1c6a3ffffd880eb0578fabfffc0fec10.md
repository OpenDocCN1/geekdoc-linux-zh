
## Navigating the Cinnamon Desktop

### STEP 5
At the bottom of the desktop there's the Panel. We've already looked at one section of the Panel, the Menu. If you right-click anywhere on the Panel, other than a Panel app, you see a menu allowing you to edit, add and set up the Panel in a different way.

![](img/7801ba6bee6a3a08f7f02897cdbcd867_32_0.png)

### STEP 6
For example, if you click the option Modify Panel, you can remove, move, remove the Panel, add a new one and clear it of any Applets that are currently present. An Applet, by the way, is an app that's designed to work and fit into the Cinnamon Panel.

![](img/7801ba6bee6a3a08f7f02897cdbcd867_32_1.png)

### STEP 7
If you right-click anywhere on the Cinnamon desktop you see a set of options that allows you to further add to, edit or view the desktop content differently. It's very similar to that of Windows, which is why Mint is a good choice for ex-Windows users.

![](img/7801ba6bee6a3a08f7f02897cdbcd867_32_2.png)

### STEP 8
From that desktop right-click, context menu, select Customize, followed by the Desktop Settings link at the bottom of the newly opened window. This opens a new window where you're able to edit which desktop icons are present. If you're using a setup with multiple monitors attached, you can also choose which monitor displays which icons.

![](img/7801ba6bee6a3a08f7f02897cdbcd867_32_3.png)

### STEP 9
Click on the Menu and type system settings and open the resulting icon. This takes you to the System Settings options. From here you're able to control and edit the way Linux Mint Cinnamon looks and works as well add new users, manage the firewall and enable accessibility options.

![](img/7801ba6bee6a3a08f7f02897cdbcd867_32_4.png)

### STEP 10
In short, Linux Mint Cinnamon can be configured to look quite extraordinary. There are many examples available of how good it can get and what can be achieved. You can go as complex or as simple as you want, adding different component and animations or just keeping it plain and easy to read.

![](img/7801ba6bee6a3a08f7f02897cdbcd867_32_5.png)

## 10 Things to do After Installing Linux Mint

Linux Mint is a polished distro out of the box but, as with most Linux distros, there are some tweaks that can be applied to improve the way it works. Although these are Mint-specific tweaks, most can be applied to other distros.

### LINUX TWEAKS

Some of these post-installation actions are highly recommended, while others are just handy additions and simply tweak the system or add a customisation.

- **STEP 1** The first, and most important, post-installation action is to update the system. Click on the shield icon in the Panel, found at the bottom right of the desktop next to the time and date. This launches the Update Manager.

![](img/7801ba6bee6a3a08f7f02897cdbcd867_33_0.png)

- **STEP 2** Linux Mint offers the user a three-level policy approach to updates: Don't Break My Computer, Optimise Stability and Security and Always Update Everything. The recommended option is the Optimise Stability and Security, which only updates safe, essential patches that won't impact critical elements of the core OS. Read through the descriptions but choose the middle, and recommended option.

![](img/7801ba6bee6a3a08f7f02897cdbcd867_33_1.png)

- **STEP 3** Click the OK button and you can see a couple of updates ready for installation. Before you update though, click on the blue bar OK button to switch to a Local Mirror. This opens the Software Sources option. In the Mirrors section, click on the Main and Base drop-down menus and select a server closest to your current location.

![](img/7801ba6bee6a3a08f7f02897cdbcd867_33_2.png)

- **STEP 4** Click the Update the Cache button and close the Software Sources window. Back in the Update Manager, click on the Install Updates icon and enter your password. The updates automatically apply themselves and relaunch Update Manager, this time with a lot more updates. Again, click Install Updates, OK any messages and wait for them to finish.

![](img/7801ba6bee6a3a08f7f02897cdbcd867_33_3.png)

- **STEP 5** The updates are graded by level, 1 being a low level update, level 5 being a dangerous one. Stick to level 3 updates, is our advice; and click **Replace** for any messages regarding overwriting a configuration file. With regards to the Software Rendering issue and lack of drivers for non-VirtualBox users, click the **Menu** and type ‘driver’ into the search box.

![](img/7801ba6bee6a3a08f7f02897cdbcd867_34_0.png)

- **STEP 6** Click the **Driver Manager** app that appears as a result of the search and enter your password. Mint takes a moment to analyse what’s available and presents you with a selection of potential drivers based on your detected hardware. Those with graphical problems, such as Software Rendering, should opt to use the latest, recommended Graphics driver.

![](img/7801ba6bee6a3a08f7f02897cdbcd867_34_1.png)

- **STEP 7** At this point you’ll probably need to restart Linux Mint, so do that now. After a reboot click the Menu button again, followed by the **Terminal**. The Terminal icon is found in the left-hand column, above the Files icon. With the Terminal open, enter: **sudo apt-get install libdvd-pkg**, press Enter and type in your password. This enables encrypted DVD playback.

![](img/7801ba6bee6a3a08f7f02897cdbcd867_34_2.png)

- **STEP 8** When asked to accept the changes, enter **Y** and also when asked to configure libdvd. Make sure **OK** is highlighted and press **Enter**, then Yes to any further questions. Next up, still in the Terminal, enter: **cat /proc/sys/vm/swappiness**; the result should be **60**. If your computer has less than **4GB** of RAM/memory, then enter: **gksudo xed /etc/sysctl.conf**.

![](img/7801ba6bee6a3a08f7f02897cdbcd867_34_3.png)

- **STEP 9** This tweak helps speed up systems with less than **4GB RAM/memory**. Scroll down to the bottom of the file you just opened and add the following new lines:

```
# Decrease swap usage to a more reasonable level
vm.swappiness=10
```

Click File > Save, then File > Quit. Reboot Linux Mint and you should notice a slight hike in performance.

![](img/7801ba6bee6a3a08f7f02897cdbcd867_34_4.png)

- **STEP 10** Security is always a concern in this modern digital age. While Linux Mint is a secure system, it’s advisable to always try and improve it. Click the Menu button and search for **Firewall**; click the **Firewall Configuration** icon and enter your password. In the Firewall window, click the **Status** slider to On.

![](img/7801ba6bee6a3a08f7f02897cdbcd867_34_5.png)

## Apollo 11

**DID YOU KNOW...**

July 20th 1969 is remembered as a turning point in human history, when mankind first stepped on the moon. The software that helped the crew make that pivotal voyage didn't even exist at the time and had to be developed from scratch. Using a new method of storing programs called Rope Memory, the engineers at MIT Instrumentation Laboratory populated the memory with a special version of assembly.

Incredibly, that code is freely available to view on GitHub. Uploaded by a researcher in 2003, you can view the code by visiting www.github.com/chrisiggaly/Apollo-11/. Look out for code snippets, such as Burn_Baby_Burn, in particular line 925 with the comment "Goodbye. Come again soon."

Have a look through, and see what else you can find.

![](img/7801ba6bee6a3a08f7f02897cdbcd867_35_0.png)

![](img/7801ba6bee6a3a08f7f02897cdbcd867_35_1.png)

> Programmers aren't without a sense a humour. See what else is in there.

![](img/7801ba6bee6a3a08f7f02897cdbcd867_36_0.png)

> One giant leap for mankind, and coding.

Credit: Apollo 11/NASA

## Creating Users

When you first install Linux Mint it is configured for use with a single user. While sharing a user account with the entire family is fine, there may come a time when you need to create separate users with their own unique Home folders.

### NEW USERS

Having different users means each user has access to his or hers own areas on the system. Documents, pictures, videos and so on are separate, as with multiple users on other operating systems.

**STEP 1** Click on the Linux Mint Menu and type 'users' to begin searching for the relevant console. From the search results, choose Users and Groups and enter your password. The Users and Groups console is quite basic looking, and thankfully easy to use. At first, you can just see your own username from when you installed Linux Mint.

![](img/7801ba6bee6a3a08f7f02897cdbcd867_37_0.png)

**STEP 2** To add a new user, click the Add button at the bottom of the console. There are two types of user you can create, Standard and Administrator. Unless the new user has need to install new apps or access parts of the file system beyond their Home folder, then opt for the Standard account type. Otherwise, use the Administrator account type.

![](img/7801ba6bee6a3a08f7f02897cdbcd867_37_2.png)

**STEP 3** Enter the new user’s Full Name, followed by the Username they need when logging into Linux Mint. Make sure the username is all in lower case, a-z and 0-9 characters only. You can have full stops, underscores or hyphens if you wish. Click the Add button when you’re ready to continue.

![](img/7801ba6bee6a3a08f7f02897cdbcd867_37_1.png)

**STEP 4** The new user appears in the list of current Linux Mint users, in alphabetical order. At present, there’s no password set so click the user in the list of current users, then click the No Password Set option under the user’s username.

![](img/7801ba6bee6a3a08f7f02897cdbcd867_37_3.png)
