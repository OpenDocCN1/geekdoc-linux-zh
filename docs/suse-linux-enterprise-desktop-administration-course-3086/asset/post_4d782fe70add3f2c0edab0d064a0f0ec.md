
# Lock Down the Desktop

Sometimes, as the administrator, you not only have to prevent certain settings from being changed, you also want to limit what users can do, such as start programs, or save files.

You can limit what users can do in two ways:

- Use GConf
- Use the Desktop Profile Editor

## Use GConf

The gconf-editor interface lists keys to lock down the desktop in the tree on the left under Desktop > GNOME > Lockdown. Keys are available that limit the access to the command line, to printing, and to dialogs used to save files.

To prevent users from changing these settings, you should configure them in the mandatory part of the GConf repository. You can open gconf-editor as root, right-click on the key, and select Set as Mandatory, or use gconftool-2:

```
da10:~ # gconftool-2 --direct --config-source xml:readwrite:/etc/opt/gnome/gconf/gconf.xml.mandatory --type bool --set /desktop/gnome/lockdown/disable_command_line true
Resolved address "xml:readwrite:/etc/opt/gnome/gconf/gconf.xml.mandatory" to a writable configuration source at position 0
```

The other keys under /desktop/gnome/lockdown are as follows:

- disable_printing
- disable_print_setup
- disable_save_to_disk

![](img/9129877170834ca9d5fdac5319bf5f12_584_0.png)

As already mentioned under “Use GConf to Set Mandatory Preference Values,” you should test these settings to make sure they work correctly. For example, although disabling the command line works as expected, disabling “Save dialogs” does not seem to have an effect on all respective dialogs.

## Use the Desktop Profile Editor

The Desktop Profile Editor (Sabayon) offers some more options to restrict users.

Start the Desktop Profile Editor; then select Edit > Lockdown in the xnest window menu. The dialog shown in Figure 14-9 appears.

![](img/9129877170834ca9d5fdac5319bf5f12_585_0.png)

### Figure 14-9

In this dialog, select the items that you want to disable.

To make the settings mandatory, select Edit > Changes in the menu of the xnest window and select the lock icon in front of the respective entries, as shown in Figure 14-10.

![](img/9129877170834ca9d5fdac5319bf5f12_586_0.png)

Figure 14-10

Save by selecting File > Save and choose the user or users these settings should be applied to. As already mentioned, these settings are copied to the user's home directory when the user logs in to GNOME and could be deleted by the user to circumvent them. If you want to avoid this possibility, set the respective keys in /etc/opt/gnome/gconf/gconf.xml.mandatory using gconftool-2.

After you have completed your configuration, test it to see if it works as expected before exposing it to public access.

![](img/9129877170834ca9d5fdac5319bf5f12_586_1.png)

## Exercise 14-4: Disable Access to the Command Line

In this exercise, you use gconf-editor to disable access to the command line on the GNOME desktop.

Use gconf-editor to make the command line unavailable on the desktop.

### Detailed Steps to Complete This Exercise

To disable the command line, do the following:

1. Try to access a command line by right-clicking on the desktop and selecting Open Terminal. This should work.
2. In a terminal window, switch to user root by entering su - (password nove11) and enter gconf-editor.
3. Browse the tree on the left to the key used to disable the command line by selecting the triangles in front of desktop and gnome; select lockdown.
4. Select (check) the key disable_command_line.
5. Right-click on the key and select Set as Mandatory.
Close the gconf-editor window.
6. Log out from the GNOME desktop. Log in again. Try to access a command line. This should no longer be possible.
7. Because you will need to access the command line in later exercises, you have to undo this change and make the command line accessible again.

   a. Switch to a text console, log in as user root (password n0v311).
   b. Enter the following command (in one line):

```
gconftool-2 --direct --config-source xml:readwrite:/etc/opt/
gnome/gconf/gconf.xml.mandatory --type bool --set /desktop/
gnome/lockdown/disable_command_line false
```

8. Return to the GNOME desktop and log out. Log in again.

## Objective 4—Customize Applications

Due to the number of applications available on SUSE Linux Enterprise Desktop, it is not possible within this course to go into any great detail on customizing them. Some, like OpenOffice.org, are so comprehensive they deserve a course of their own.

However, as desktop administrator, you should understand how applications usually store their configurations and you should be able to provide users with useful configuration defaults.

The /etc/skel/ directory contains all the files that are copied to a new user's home directory when the account is created.

By default, this directory already contains various configuration files (such as .bashrc) or directories (such as Desktop, bin, or public_html). As an administrator, you can add files or directories to /etc/skel/ that you want to see in the home directories of new users.

Configuration files or directories are usually hidden, which means that their name starts with a '.'. These files are ASCII files, which can be edited with any text editor. However, it is preferable to use the respective application to write the configuration and to use the resulting file as a template. This template is then copied to /etc/skel/ or to the home directory of another user.

This objective covers two examples of configuration settings that can be made available to all users:

- OpenOffice.org 2.0
- Firefox

Other applications, like Evolution, require a configuration on a per-user basis that does not lend itself to this approach.

## OpenOffice.org 2.0

The following topics are covered for OpenOffice 2.0:

- Language Settings
- Templates

### Language Settings

Depending on the user's language, you might want to change OpenOffice.org's menu language. Many different languages are available, but they are contained in separate packages that you have to install. German, for example, is contained in the OpenOffice_org-de package, while French is in OpenOffice_org-fr.

To install a language, open a terminal window and enter, as root, yast2 sw_single, search for Office and select the package for the desired language. If spell check dictionaries are available for the selected language, they are installed automatically as well.

Then start OpenOffice.org and select Tools > Options > Language Settings > Language. In this dialog, you can select the language for the user interface and the locale, as well as the default language for documents.

Within a user's home directory, the configuration directory for OpenOffice.org on SUSE Linux Enterprise Desktop 10 is ~/.ooo-2.0. The above settings are written to the Setup.xcu and Office/Linguistic.xcu files in the ~/.ooo-2.0/user/registry/data/org/openoffice/ directory.

### Templates

Companies usually develop their own templates for business letters, presentations, forms, or other company-specific documents. It is easy to make these available to OpenOffice.org users.

OpenOffice.org looks for templates in subdirectories of the system wide /usr/lib/ooo-2.0/share/template/language/ directory and in the user's home directory in ~/.ooo-2.0/user/template/.

As system administrator, you can store the templates in a Companyname directory in the systemwide OpenOffice.org template directory. Users can store any templates they need in the template directory in their home directories. If a user selects File > New > Templates and Documents > Templates, the user will find the company templates in a directory (e.g., Digitalairlines), while those in the user's home directory are accessible via the entry My Templates. See Figure 14-11.

![](img/9129877170834ca9d5fdac5319bf5f12_588_0.png)

Figure 14-11

Templates can be stored in any other directory as well. To make them available within OpenOffice.org, select Tools > Options > OpenOffice.org > Paths > Templates and add that location in the dialog that opens up.

You can copy a sample .ooo-2.0 directory with company-specific OpenOffice.org settings to /etc/skel/ to make all configuration settings and templates in that directory available to new users.

![](img/9129877170834ca9d5fdac5319bf5f12_589_0.png)

A helpful resource for OpenOffice.org is http://www.oooforum.org/.

## Firefox

Firefox can be configured extensively via Edit > Preferences. Several tabs cover various aspects of the configuration. See Figure 14-12.

![](img/9129877170834ca9d5fdac5319bf5f12_589_1.png)

Figure 14-12
