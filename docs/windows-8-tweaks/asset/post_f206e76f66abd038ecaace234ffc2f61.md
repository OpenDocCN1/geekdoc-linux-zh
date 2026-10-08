
# Boot To Desktop

One of the more controversial changes in Windows 8 is the behavior after you log in. Instead of viewing the desktop, users are shown the new Start screen. If you want to view the desktop you must select the Desktop tile. Microsoft is trying hard to promote the new windowless immersive environment and that has rubbed some users the wrong way.

Adding fuel to the fire, Microsoft blocked the easy methods to change this behavior and go directly to the desktop after logon in the final builds of Windows 8. The only method that remains requires third-party software to work around the limitations imposed by Microsoft.

I spent a lot of time investigating how to solve this problem and ended up writing a free utility called Tweaks.com Boot to Desktop. My utility has two main components. The first part is a tiny service that runs in the background and monitors for when the logon event happens. When that is detected, it launches a second component under the user context that does the leg work of showing the desktop. The solution is rather complex, but was necessary to get around the limitations imposed by Microsoft.

Using my utility is very simple. Just download it from tweaks.com/414700 and install it. After a reboot you will boot directly to the desktop.

If you change your mind, you can uninstall the utility just like any application and you will revert to the Start screen behavior.

# Summary

You can think of this first customizing chapter as the first step in the complete customization of every possible aspect of your Windows 8 install. You started with tweaking the way the logon screen behaves and then made some major changes to the look by changing the lock screen.

The next chapter helps you customize the user navigation components of Windows 8. First, you learn all about customizing the Start screen. Then you learn how to customize the next most used component of Windows 8—the taskbar.

## Customizing User Navigation

Customizing user navigation is the next stop on the Windows 8 customizing road trip. In the previous chapter, with the help of some cool tweaks, you were able to change and improve the logon experience. This chapter picks up where Chapter 5 left off and shows you how to customize and improve the visual navigation elements of Windows 8.

This chapter starts with customizing the look and the content of the cool new Start screen, formally the Start menu. The improved Start screen in Windows 8 has many useful features, and I show how you can use them best. Then, I show you how you can customize almost everything you see on the Start screen. If you don’t like the new Start screen, I show you how to get the old classic Start menu back.

You also learn how to customize the taskbar on the bottom of your screen. The taskbar is an essential part of navigating your computer. I show you how to customize and improve its features and give you some new ideas about how you can use it to dramatically improve your experiences with Windows 8.

## Customizing the Start Screen

Completely revamped for Windows 8, the Start screen enables you to search your programs and jump directly to various components of Windows. Additionally, you can launch commands much as you could in the traditional Run box by just typing them in.

After you finish reading these next few sections, you will have transformed your Start screen into something that works better for you and is much more useful for your everyday tasks.

### Changing the Background and Colors

Changing the background is one of the easiest customizations, but it makes a big impact on personalizing your Windows 8 PC. You can use two methods to customize the Start screen background: one using native functionality that limits you to designs created by Microsoft, and another using third-party utilities to use any image as the background image.

*   **Native Background Personalization**

    Microsoft provides 20 different background images along with 25 different color schemes. That means 625 possible combinations of each background and color scheme are available. With that many combinations, the odds are in your favor to find something that you like using the native personalization options.

    Selecting your background image and color scheme is very easy in Windows 8:

    1.  Open the Start screen and type **customize**.
    2.  Click the Settings filter.
    3.  Click Customize Your Start screen.
    4.  Pick the background image you want to use, as shown in Figure 6-1.
    5.  Pick the color scheme you want to use.

    As soon as you make the change, your settings are saved. The preview window gives a nice simulated view, but I always like hitting the Windows Key to check out the real deal.

    ![](img/ea75090cfee8ac890f64c8c4f62f7285_92_0.png)

*   **Background Customization with Utilities**

    If you are not happy with the images and colors Microsoft included in Windows 8, you must use third-party utilities for more options. The following are two utilities that I have used with Windows 8 to customize the Start screen image and colors further.

    **Stardock Decor8**

    Decor8 is by far the best Start screen customizing application. You can set any image as your background, customize the colors of your tiles, and tweak the visual effects. The interface is easy to use and it even includes advanced features that enable you to automatically change the background image on a timer. The only downside to this app is that you must pay $4.99 to use it.

    Head over to tweaks.com/157844 and download a free 30-day trial. After Decor8 is installed, you see the main customization screen as shown in Figure 6-2.

    ![](img/ea75090cfee8ac890f64c8c4f62f7285_93_0.png)

    **Figure 6-2:** Stardock Decor8 offers this customization screen.

    Select one of the background images or click Select File to use your own. Click the Colors option on the left menu to select from the standard Windows color schemes or create your own.

    **Windows 8 Start Screen Customizer**

    The Windows 8 Start Screen Customizer is a free utility written by vhanla, who is known for creating a number of free Windows customization utilities. Although it does not have all of the bells and whistles of Decor8, it gets the job done in enabling you to replace the Start screen background image. Unique to the Windows 8 Start Screen Customizer, you can also adjust the transparency of the entire Start screen.

    You can download a free copy at `tweaks.com/161004`. Just extract the file and rename the extension from `.ex_` to `.exe` and then run. Once you have it up and running, select one of the default backgrounds or click Load Picture to select your own. Then just drag the border box around the section of the picture you want to use, click the Apply & Save button as shown in Figure 6-3, and your new Start screen will be active.

    ![](img/ea75090cfee8ac890f64c8c4f62f7285_94_0.png)

    Figure 6-3: Windows 8 offers a Start Screen Customizer.

## Working with Live Tiles

Tiles make up all the content on the new Start screen in Windows 8. Knowing how to customize them will help you personalize your Windows 8 experience. Over time as you install more and more apps, the Start screen can become cluttered. Finding what you want becomes difficult and the result is a visual mess. Windows 8 has some very useful organization tools built in, but they are not always intuitive because Windows 8 puts a lot of options in hidden menus.

### Adding or Removing Tiles

Anything that shows up in the Start screen application search can be pinned to the main Start screen. An easy method to view all apps on your computer, similar to the old All Programs menu in the old Start menu, is to open the Start screen, right-click, and then select All Apps on the pop-up charms bar.

At that point just scroll until you find the application you want to pin and right-click it. Then Select Pin To Start as shown in Figure 6-4.

![](img/ea75090cfee8ac890f64c8c4f62f7285_95_0.png)

Figure 6-4: Pin an application to your Start screen.

Removing tiles is even easier. Simply right-click a tile on your Start screen and select Unpin From Start.

### Moving Tiles

Customizing the location of the tiles is one thing that Microsoft made easy in Windows 8. With a mouse, just click and hold a tile and you can drag it anywhere you want on the Start screen. With a keyboard, select a tile with the tab key, then hold down Shift+Alt and use the arrow keys to move tiles around.

### Grouping Tiles

After you install a lot of apps on your PC your Start screen will become cluttered. Sorting your tiles into groups is absolutely necessary to keep your Start screen organized and under control. You can arrange tiles in any number of groups and you can label the groups. The process of creating groups is fairly straightforward.

Create a group by dragging a tile in one of the default groups to the left or right of the current group. As you drag the tile out of a group, a new group indicator displays as shown in Figure 6-5. Drop the tile on the vertical indicator and it is placed in a new group. Next, just drop additional tiles into the group as necessary.
