
## Customizing the Notification Area

Over the years the notification area, previously known as the system tray, has become more and more cluttered. It seems as though just about every application you install wants to create a notification area icon when it is running. In Windows 8, Microsoft decided enough is enough and cleaned up the notification area by creating a new overflow container. Now when any application creates a notification area icon, it does not show up by default. Instead, you have to click the arrow on the end of the notification area to view the overflow container. Then if you decide that the notification area icon actually is useful, you can drag it from the overflow container to the main notification area. Now you are in full control of your notification area and can keep it nice and neat or cluttered depending on how you like it.

In the next few sections I show you how you can fine-tune your notification area by customizing the appearance and behavior.

## Hiding Icons

As I mentioned earlier, the only additional icons that appear in your notification area are icons that you personally drag into it. If you want to hide any of those icons, including the default system icons, you can simply drag them off it and they will fall in the overflow container. This works great most of the time, but there is another way to get more control:

- 1. Click the arrow to the left of the notification area and then select Customize.
- 2. This loads the Notification Area Icons Control Panel screen where you can fine-tune each icon that ever attempted to load in the notification area. Scroll through the list and select the behavior you want to use for each icon. You can choose from Show Icons And Notifications, Hide Icons And Notifications, and Only Show Notifications.
- 3. After you have adjusted all your icons, click OK.

## Removing System Icons and the Clock

Tweaking the system icons such as the Volume, Network, and Clock icons requires an additional step. Follow these instructions to hide any of the default system icons:

- 1. Click the arrow to the left of the notification area and select Customize.
- 2. When the Notification Area Icons Control Panel screen loads, click Turn System Icons On Or Off.
- 3. For each system icon, toggle the drop-down list to turn each item on or off.
- 4. Click OK when you are finished.

## Restoring the Start Button

The removal of the Start button was one the boldest changes to Windows in years. After training users that is where you click to start any application for more than fifteen years, Microsoft decided to throw away that longtime behavior and introduce the “hot corner” to display the Start screen. We can speculate on their intentions, but the fact remains that many people liked having a button to click to display the Start menu.

In some situations the new “hot corner” makes using Windows more difficult. I am a big user of virtual machines that display the running OS in a window on my desktop. When I run a Windows 8 virtual machine, it is very difficult to move the mouse into the lower-left corner to bring up the Start screen. Often I move the mouse too far outside of the window of the virtual machine.

Driven by my own annoyance with the lack of a Start button, I set out to create a Start button replacement. The result of that effort was the Tweaks.com Start utility. It is a simple application that you pin to your taskbar but has a lot of useful features. Clicking it shows the Start screen, but that is just the beginning. You can select which view of the Start screen you want to see. The application view as shown in Figure 6-17 and the zoomed-out group view as shown in Figure 6-18 are available in addition to the default Start screen view. My personal favorite is the Start screen groups view because as the number of apps on the Start screen grows, you can easily jump to a group by just clicking it instead of scrolling to the right forever.

I also created a useful right-click Jump List for my Start button replacement that put the most common tasks that are tucked away in Windows 8 within a click. You will find that basic commands such as shutting down your PC and administrative utilities are easy to access.

The best part is that customizing the Start button icon is very simple. Just open up the Configuration window found on the top of the Jump List and change the icon to any icon in a DLL or ICO file.

Tweaks.com Start is a free utility that you can download from tweeks.com/655582. Just install and follow the on-screen instructions to configure.

![](img/ea75090cfee8ac890f64c8c4f62f7285_111_0.png)

Figure 6-17: Create this Start screen Application list view.

![](img/ea75090cfee8ac890f64c8c4f62f7285_111_1.png)

Figure 6-18: Use this Start screen group view.

## Using Group Policy Editor to Customize the Start Screen and Taskbar

The Group Policy Editor is a great component of Windows that enables you to make dozens of advanced setting changes that are hidden from normal users. The Group Policy Editor works by enabling you to define various rules, called the *policies*, which tell Windows how to behave.

The collection of policies is known as Group Policy, of which there are two types: local and domain based. Local is when the policy resides in and is controlled on the local computer. A domain-based policy is a policy that resides on an Active Directory domain controller to which multiple computers are connected. Domain policy is primarily used only in businesses that need a way to control multiple computers from a central location. In this book, some tweaks use local Group Policy to configure the Start menu because most of you are customizing your home computers and do not have them connected to a Windows domain. The actual policies and way you set them are the same for both types of group policies, so you can apply these same techniques to a domain policy if desired.

The policies are set and modified using the, you guessed it, Group Policy Editor. This is the tool that you will be using to set the policies to help you customize the Start menu. First, you learn how to use the policy editor, and then all the policies relevant to customizing the Start menu.

### Setting Policies with the Group Policy Editor

Using the Group Policy Editor is a lot like using the Registry Editor. It is based on a hierarchical structure of sections that all policies are organized within. All policies are divided into two sections: Computer Policies and User Policies. Computer Policies are settings that apply to components of Windows such as hardware and global feature settings. User Policies are settings that can vary between users on a computer. This is where most of the policies that you will use to customize the look of your interface are located.

Now that you know the basics of the Group Policy Editor, dive in and start using the policy editor:

- 1. Open the Start screen, enter `gpedit.msc` in the Search box, and press Enter.
- 2. After the Group Policy Editor has loaded, you see the hierarchical structure and Computer and User policies sections mentioned previously.
- 3. Navigate through User Configuration, Administrative Template, and then select Start Menu and Taskbar.
- 4. You see a list of all policies that you can configure. Right-click a policy that you want to configure and select Edit.
- 5. On the policy screen, select the option to turn on the policy or set the policy value, and then click OK, as shown in Figure 6-19.
- 6. Exit the policy editor and log off and back on. Some policy changes may require a reboot.

![](img/ea75090cfee8ac890f64c8c4f62f7285_113_0.png)

**Figure 6-19:** Configure a policy in the Group Policy Editor.

Now that you know how to use the Group Policy Editor, the next section shows you all the policies and briefly describes what they do.

## Changing Start Screen and Taskbar Policies

A lot of policies listed under the Start Menu and Taskbar section are not relevant to Windows 8. Consider those junk that Microsoft forgot to remove because they will have no effect on Windows 8. Or maybe Microsoft wanted to make it easy to create policies for older versions of Windows. Table 6-1 shows a list of some useful group policies for Windows 8 that will help you customize the Start screen and the taskbar.
