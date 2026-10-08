![](bbox=[0.12, 0.07, 0.86, 0.15])

You enable small icons in the Taskbar properties:

+   1. Right-click the taskbar and select Properties.
2. On the Taskbar tab, check Use Small Taskbar Buttons.
3. Click OK or Apply to see the result.

# Tweaking Taskbar Preview Delay

Taskbar previews have been improved in Windows 8, enabling you to take a quick peek at a window by hovering over its taskbar icon. My biggest complaint is the delay before the taskbar previews are shown. I want to use the new features but the amount of time I have to hover over a taskbar application is too long. You can tweak this with a simple registry hack:

+   1. Open the Start screen, type **regedit**, and hit Enter.
2. When the Registry Editor is started, navigate through HKEY_CURRENT_\USER, Software, Microsoft, Windows, CurrentVersion, Explorer, and Advanced.
3. Right-click Advanced, click New, and then click DWORD (32-bit) Value. Name the new value **ExtendedUIHoverTime**.
4. Right-click the new ExtendedUIHoverTime value you just created and select Modify.
5. Change the Base to Decimal and enter the new value in milliseconds and click OK. The default value is 400 in the decimal base, which is 400 milliseconds. I like to set mine to 100.
6. Reboot and test your new setting.

# Restore Classic Quick Launch Bar

The classic Quick Launch bar was a great way to start your programs in previous versions of Windows. With the new taskbar in Windows 8, the Quick Launch bar was removed and replaced with the application pinning feature. The ability to pin an application to the taskbar is nice, but it does not exactly replicate the old behavior of the Quick Launch bar.