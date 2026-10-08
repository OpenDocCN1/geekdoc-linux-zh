
![](img/ea75090cfee8ac890f64c8c4f62f7285_56_0.png)

Docked in bars that appear on all sides of the screen, the most commonly used charms are the system charms, as shown in Figure 3-5. The system charms are universal to any application you have open and even exist on the classic desktop. If you have a touch device, just slide your finger inward from the right side of the screen. Desktop and laptop users must put the mouse cursor in the top-right corner of their screen and then move down as the charms show up. Alternatively, you can hit Windows Key+C to bring up the system charms.

The system charms bar enables you to open the Start screen, search everything or just the app you currently have open, and open the Settings panel, where you can shut down your PC. Why Microsoft buried the ability to turn off and reboot your computer in the settings charm is beyond me, but at least now you know how to turn your PC off properly.

Within Windows Store apps or on the Start screen are additional charms in application bars on the top and bottom of the screen. Drag your finger from the top of the screen down or from the bottom of the screen up, or if you have a mouse just right-click. These are the new application-specific context menus that are docked to edges of the screen. They enable you to perform tasks, such as opening a new tab in Internet Explorer, or access tile settings for a selected tile on the Start screen as shown in Figure 3-6.

![](img/ea75090cfee8ac890f64c8c4f62f7285_57_0.png)

**Figure 3-5:** System charms display information when you need it.

![](img/ea75090cfee8ac890f64c8c4f62f7285_57_1.png)

**Figure 3-6:** The Start screen has Tile Settings charms.

The last type of charm is located on the left side of the screen and helps you switch between apps. Think of this as the taskbar of the new interface. Drag your finger inward from the left side of the screen or place your mouse cursor on the top-left corner of your screen and then move the cursor down. Alternatively, on a keyboard you can hit Windows Key+Tab. This charm provides a thumbnail view of all your open Metro style applications and a screenshot of your desktop.

## Using Keyboard Shortcuts in Windows Store Apps and the Start Screen

I already covered a few of the keyboard shortcuts that help you fly around the new interface if you don't have a touch device, but you can use a lot more. The keyboard shortcuts in Table 3-1 will save you a few clicks and get to items that are ordinarily buried within the interface.

**Table 3-1: Windows Store Apps and Start Screen Keyboard Shortcuts**

| KEY COMBINATION | FUNCTION |
| :--- | :--- |
| Windows Key | Opens the Start screen |
| Windows Key+Tab | Metro app switcher |
| Windows Key+C | System charms |
| Windows Key+Z | Application charms |
| Windows Key+I | Settings menu |
| Windows Key+K | Devices menu |
| Windows Key+H | Share menu |
| Windows Key+F | Search files on Start screen |
| Windows Key+Q | Application search on Start screen |
| Windows Key+W | Settings search on Start screen |
| Windows Key+. (period) | Snap Metro app to the right side of the screen |
| Windows Key+Shift+. (period) | Snap Metro app to the left side of the screen (only works on wide-screen monitors) |

## Using the Classic Desktop

Although the new Metro interface gets most of the attention when talking about Windows 8, the classic desktop also received some minor refinements. Almost all of the changes are cosmetic because the underlying system components are almost identical to Windows 7, just optimized.

### What's New?

The new desktop features are centered on Windows taskbar and the File Explorer interface. Users will instantly recognize the familiar ribbon interface from Microsoft Office that has been integrated within File Explorer. Love it or hate it, many new options are just a click away. The file copy/move dialog box also got a big update with a pretty graph and the ability to pause file transfers, which can be very helpful, as shown in Figure 3-7.

![](img/ea75090cfee8ac890f64c8c4f62f7285_59_0.png)

**Figure 3-7:** The new Windows Copy dialog box offers a pause option.

The Windows taskbar finally received multi-monitor support, which allows users to extend it to all monitors. Users can also customize the behavior of application icons so that open windows on a single monitor show up on all monitor taskbars or just on the taskbar the window is actually on.

Under the covers, Windows continued the Vista diet. According to Microsoft, Windows 8 uses less RAM than Windows 7 and has fewer processes running in the background. I have actually used Windows 8 on a machine with just 2 GB of RAM and performance was acceptable.

## Using Desktop Keyboard Shortcuts

Navigating the classic desktop in Windows 8 has not changed significantly other than how you get to it. The keyboard shortcuts in Table 3-2 are not all brand new, but they will help you quickly navigate the interface like a true power user.

Table 3-2: Classic Desktop Keyboard Shortcuts

| KEY COMBINATION | FUNCTION |
| :--- | :--- |
| Windows Key+D | Show desktop |
| Windows Key+Comma | Peek at desktop |
| Windows Key+M | Minimize window |
| Windows Key+Up Arrow | Maximize window |
| Windows Key+Right Arrow | Snap window right |
| Windows Key+Left Arrow | Snap window left |
| Windows Key+X | Admin tools menu |
| Windows Key+Pause/Break | System Information |
| Ctrl+Shift+Escape | Task Manager |
| Windows Key+Enter | Windows Narrator |
| Windows Key+L | Lock PC |
| Windows Key+P | Projector options |
| Windows Key+Print Screen | Saves screenshot to pictures |
| Windows Key+Space | Switch language packs |
| Windows Key+R | Run dialog |
| Windows Key+E | File Explorer |
| Windows Key+Number | Launch pinned taskbar app |
| Windows Key+Plus | Screen zoom in |
| Windows Key+Minus | Screen zoom out |

## Summary

This chapter covered the basics of what is new in Windows 8 and how to use it like a power user. The new interface takes some time to get used to, and in the chapters to come I cover customizing it if you are a fan. If not, I show you how to avoid it as much as possible.

In the next chapter I cover how to safely tweak your computer. Starting very soon you will be modifying the system, which always involves the risk of something going wrong, so it is important to know how to make changes safely.

# **CHAPTER 4**

# **Safe Tweaking**

If your computer came with Windows 8 preinstalled, or you have finished installing Windows 8, you are almost ready to begin tweaking. But first, this chapter talks about the safe way to tweak and customize your computer. Many tweaks, tips, and secrets can create severe problems if you accidentally miss a step. That is why this is a good time to discuss some of the ways you should protect your computer, so you can easily undo any tweak that causes problems.

To get started, you create Restore Points that enable you to take a configuration snapshot so you can easily jump back to a prior state. Then this chapter covers Windows Backup to protect your data, and Startup Repair to automatically fix issues that may prevent Windows 8 from starting up. Additionally, I cover the new one-click refresh and reset features that automatically restore Windows to a working state.

## **Using System Restore**

System Restore has matured into something very valuable for any power user who tweaks his computer. Every time you make a change, there is a risk that something could go wrong. Wouldn't it be nice if you could easily undo any change with just a few clicks? System Restore provides the solution to that problem by enabling you to jump back in time to an earlier state.

In the next sections I show you how to create Restore Points before you tweak and then how to restore to a previous state if something goes wrong.

### Creating Restore Points

You can create Restore Points in Windows in a number of ways. Every time you install new software, Windows automatically creates a new Restore Point. You can also manually create Restore Points in Windows. This chapter starts with the normal way and then shows you how to create a desktop shortcut that enables you to jump directly to the Create Restore Point screen. To get started, do the following:

- 1. Open the Start screen, type **Create a Restore Point**, switch to Settings filter, and then hit Enter.

The System Properties System Protection tab, shown in Figure 4-1, opens. This enables you to view your System Restore settings and create Restore Points.

![](img/ea75090cfee8ac890f64c8c4f62f7285_63_0.png)

**Figure 4-1**: Access your System Restore settings.
