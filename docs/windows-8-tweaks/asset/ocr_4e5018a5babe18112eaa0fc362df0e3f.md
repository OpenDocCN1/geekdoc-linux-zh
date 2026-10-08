WindowBlinds, to customize the look of your computer. This will help you take customization to the next level.

# # Using Hacked Visual Styles

Windows 8 uses an enhanced skinning engine based off the engine found in Windows XP to display the non-glass interface as well as the new glass DWM interface. In Windows XP, the visual style engine used bitmaps stored in a resource file. The visual style's resource file contains all visual elements, such as images of buttons and window components as well as some configuration files. In Windows 8, the resource file has been modernized to include PNG images instead of bitmaps and is updated for the new interface design.

You create visual styles for Windows 8 the same way you do for Windows XP, Vista, and Windows 7. You start with an existing visual style, such as the default visual style that is included in Windows 8, and use a resource hacking tool to replace the images within the file. After you have replaced all the resources in the file with PNG replacements and created a new visual style file, you are almost ready to use the hacked visual style.

The last step before you can use any visual style that you downloaded or made yourself is patching the skinning engine files. The skinning engine in Windows 8 will use only visual styles that have a Microsoft digital signature on the file. Visual styles that you make yourself by editing the resources or other visual styles that you download from the Internet no longer have a valid Microsoft digital signature because the file content has changed. To use hacked visual styles in Windows 8 you need to patch the system files that impose this digital signature requirement on visual style files.

Thankfully, a number of users have released utilities that patch the digital signature requirement. One that I'm going to show you is called UxStyle Core written by Rafael Rivera. This utility patches the digital signature requirement in memory so it does not modify any files on your computer. The only catch is that UxStyle for Windows 8 supports only 64-bit systems.

Before you get started using UxStyle Core, you need to download some Windows 8 visual styles to skin the interface. The following are some sites that I recommend to find compatible visual styles:

+   - DeviantArt Visual Styles—tweaks.com/925782

+   - DeskModder—tweaks.com/167845

+   - Windows 8 Themes—tweaks.com/351086

Make sure you download only visual styles created for Windows 8. Windows Vista and Windows XP visual styles are not compatible. After you