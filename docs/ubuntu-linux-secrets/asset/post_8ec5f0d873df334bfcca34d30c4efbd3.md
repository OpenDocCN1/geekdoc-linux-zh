
window, which appears before the final wizard window, for setting individual options).

+   5. Define a printer name for the printer, and add the optional description and location if you want to include more information about the printer.

+   6. Click Apply in the Summary window to finish adding the new printer.

The new printer is added as an icon in the Printer Configuration window (even if you mapped to a remote printer). You should now see the new printer when printing from applications on your system. However, before getting too carried away with printing, it’s a good idea to check how the printer is configured.

## Modifying Printer Properties

You can modify the properties of any printer on the system, whether Ubuntu automatically created it or you manually created it. If you double-click the icon for the printer you want to configure, the Printer Properties window appears, as seen in Figure 15-4.

![](img/39e65eeb4f54001ede08c6114ae3cc6c_401_0.png)

Figure 15-4: Modifying printer properties in the Printer Configuration tool.

The window on the left contains five main properties groups that contain printer information you can modify. The main groups are

- Settings
- Policies
- Access Control
- Printer Options
- Job Options

Some printers contain a sixth group for setting specific options for the printer. In the next sections, we take a closer look at each of the main groups.

## Settings

The Settings group provides some basic settings you can change for the printer. From here, you can change the description and location tags for the printer, the URI of the printer, and the PPD file used for the printer.

There are also three other buttons that you can use:

- Print Test Page: Provides an easy way for you to test whether the printer and PPD file are working properly.
- Print Self-Test Page: Some printers support an internal self-test page. If your printer supports that feature, this button will be enabled.
- Clean Print Heads: Some printers support an external command to clean the print heads. If your printer supports that feature, this button will be enabled.

That covers the general settings for the printer. The other groups provide more advanced settings.

## Policies

The Policies group contains three separate sections. The State section allows you to control the state of the printer:

- Enabled: Lets you take the printer offline if there's a problem.
- Accepting Jobs: Allows you to temporarily suspend processing print jobs.
- Shared: Allows you to set whether the printer is a shared resource on the network.

There are four policies (or rules) that control printer behavior. Two of the policies control banner pages for print jobs; the other two control how the printer operates.

There are two operation policies that you can set:

- Error Policy: Determines how the printer reacts to an error in the printing process. The choices are Abort-Job (giving up on printing the job), Retry-Job (trying again after manual intervention), or Stop-Printer (preventing all other print jobs from printing). The default value is to retry the job because the problem most likely can be resolved with an easy fix, such as turning the printer on or setting it as online.
- Operation Policy: Determines the mode the printer runs in. At this time, the only setting is default.

Banner pages allow you to print a special page describing the print job. The Starting Banner page prints out before the print job. This option allows you to print a cover sheet for the print job. Theoretically, it's supposed to provide some privacy, blocking people from seeing the first print page on the printer, but, really, who wouldn't just look under the banner page? There are several banner pages you can choose from.

The Ending Banner page allows you to print a page that signifies the end of the print job. If you're in a high-volume printing environment, using a starting or ending banner helps keep everyone's print jobs separate. In a workstation environment, it's pretty much a waste of paper. The default is to not print either of the banner pages.

## Access Control

The Access Control group provides a method for you to restrict access to the printer. There are two ways to do this.

First, you can list every user account that the server will prevent from using the printer. This option means that any user not on the list can print and that any user on the list can't print.
