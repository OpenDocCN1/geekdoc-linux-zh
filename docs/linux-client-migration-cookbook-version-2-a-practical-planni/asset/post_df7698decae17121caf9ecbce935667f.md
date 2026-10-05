
![](img/23b949da14ff7bab8762f0f0361af394_307_0.png)

Figure C-1 Progression Desktop neutralization process

## GUI

The GUI allows users to perform the migration via a “Next-Next-Finish” style wizard interface. The user is presented with a series of questions that ask which system settings, application settings, and files from the Windows desktop should be captured and stored for migration. For instance, in Figure C-2 on page 281, a list of detected applications is shown, and the user is choosing to migrate settings from Microsoft Outlook, AOL Instant Messenger, Microsoft Internet Explorer, and Microsoft Word.

![](img/23b949da14ff7bab8762f0f0361af394_308_0.png)

Figure C-2 Progression Desktop storing settings on Windows

Next, on the Linux desktop, the user interfaces asks to which destination applications and locations those settings should be applied. In Figure C-3 on page 282, the application is asking for settings that were stored in Figure C-2. The user has chosen to map Microsoft Internet Explorer to Mozilla Firefox, AOL Instant Messenger to GAIM, Microsoft Outlook to Novell, and Microsoft Word to OpenOffice.org Writer.

Appendix C. Automating desktop migration using Versora Progression Desktop 281

## Progression Desktop

Application Settings Destinations

Please select the applications whose settings you wish to apply. You can use the drop down menu to select an appropriate destination for applications that can be applied to multiple destinations.

If you do not wish to migrate an application, you may select the "Do Not Migrate" option for that application.

| Application | Destination |
| :--- | :--- |
| AOL | AOL Instant Messenger |
| GAIM | |
| Microsoft | MSN Messenger |
| Microsoft | Excel |
| Microsoft | OpenOffice.org Calc |
| Microsoft | Outlook |
| Microsoft | PowerPoint |
| Microsoft | OpenOffice.org Writer |

Go Back
Continue

![](img/23b949da14ff7bab8762f0f0361af394_309_0.png)

### Progression Desktop settings on Linux

Performing a migration using the GUI is the simplest. However, because this option requires some setup, it is best suited for smaller groups. For larger groups, you should consider the command line.

### Command line

Templates are defined in XML files which tell Progression Desktop what items are to capture and where to place them. Because the GUI is not available on all systems, the command line interface allows you to automate the migration. This approach is also best suited for environments where a GUI is not available or is not desired.

 desired.

The general steps for migration that are available on all platforms are:

- 1. Create a template.
- 2. Create the Platform Neutral Package.
- 3. Apply the Platform Neutral Package.

## Desktop architecture

One of the major design goals of Progression Desktop was extensibility. With many unique choices of applications in both Windows and Linux for each of the common and targeted data sets, Progression Desktop needed to be able to migrate to several different configurations. For instance, a user who had been running Microsoft Outlook might want to migrate to Evolution, while another user might migrate from Mozilla Mail to Thunderbird. In order to achieve this goal and be able to run on both Windows and Linux, Progression Desktop utilizes a plug-in-based architecture and XML data files running on the .NET platform. The three main technologies developed for this are the PNP file format, the Settings Packages, and the plug-ins as Transforms and Accessories.

## PNP Files

Progression Desktop stores extracted settings in a Platform Neutral Package, or PNP. PNP files are a standard Zip file, which can be opened with your favorite Zip editor, such as FileRoller, Ark, or WinZip. Figure C-4 on page 285 shows
