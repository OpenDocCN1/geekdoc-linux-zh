
## The Desktop Menu

Right-clicking on a blank spot on the desktop will bring up a menu with several options (see Figure 18.7).

FIGURE 18.7
The Desktop menu in KDE can be activated by right-clicking on a blank area of the desktop.

![](img/ba0161b65b37e94cffc801ecbacaba5e_319_0.png)

Here is what the options in the menu do:

- **Create new.** This option allows you to create new links on the desktop, which are basically the same thing as shortcuts in Windows. You can also create new directories on the desktop, open a new text file in the text editor for editing, and so on.
- **Bookmarks.** This option provides quick access to your bookmarked Web sites. Bookmarks in Netscape and KDE's built-in Web browser are automatically imported into this menu.
- **Paste.** Pastes a copied item onto the desktop (a file, for example).
- **Help on desktop.** Brings up the KDE help center, which can be browsed like a Web page.
- **Configure background.** Allows you to change the background color or image of the desktop. We will cover more on this later on.
- **Configure desktop.** Allows you to customize various features on the desktop. We will talk more about this later on.
- **Enable desktop menu/Disable desktop menu.** This is a toggle. When enabled, a menu bar is displayed across the top of the desktop that enables you quick access to bookmarks, open windows, help functions, and so on. Clicking this option again turns off the desktop menu.
- **Unclutter windows.** This option attempts to arrange the windows on your desktop in an orderly manner.
- **Cascade windows.** Performs the same function as the Microsoft Windows equivalent. It arranges the windows on the desktop in a cascading style.
- **Line up icons.** This option lines up the icons in an orderly fashion. They will be lined up in whatever order they are closest to now.
- **Arrange icons.** This option arranges the icons down the left side of the screen.
- **Lock screen.** This option blanks the screen and locks the desktop. To unlock it, you need to enter your password.
- **Logout.** This option logs you out of the KDE desktop. However, you will still be logged in to FreeBSD.

## KDE Applets

Applets are basically miniature applications bundled with KDE. Many of them can be accessed from the Utilities menu off of the K menu. For example, there is a calculator here, as well as an address book. The calculator is pretty self-explanatory, but the address book is a neat little utility that eases the use of KMail, the KDE email program, by integrating contact addresses into it and other KDE applications such as the Konqueror Web browser. We will look at the address book next.

## The Address Book

Figure 18.8 shows the KDE address book. The first time you start it, you will be given a couple of messages telling you that it is creating your personal address files and such. You will only see these messages the first time.

FIGURE 18.8
The KDE address book.

![](img/ba0161b65b37e94cffc801ecbacaba5e_320_0.png)

Because no entries are currently in the address book, most of the options are grayed out. To add an entry, you can either click on the first icon in the icon bar that looks like a piece of paper, or you can click on the Edit menu, and then Add Entry.

To search for an entry, click on the magnifying glass icon. This will bring up a search box like the one shown in Figure 18.9.

**FIGURE 18.9**
*Searching for an entry in the KDE address book.*

![](img/ba0161b65b37e94cffc801ecbacaba5e_321_0.png)

Choose which key you want to search by (last name, first name, and so on.) Then enter the search term in the ...Matches... box. You can use wildcards here if you want to match multiple entries or if you aren't sure of exactly what you are looking for. For example, if you are searching by last name, and you enter a* here, all people whose last name begins with a will be matched. If you enter a????, all people whose last name begins with a and contains four additional characters after it will be matched.

Note that the address book also allows you to search by regular expressions. Regular expressions, also known as regexps, are a mechanism for constructing complex, variable-based searches. A full discussion of how regexps work is beyond the scope of this book. However, a brief glance at some of the features of a regexp is shown here:

- `.` Matches any character
- `[abc]` Matches any of a, b, or c
- `[a-z]` Matches any characters in the range a-z
- `*` Matches any number of consecutive times (including zero)
- `+` Matches one or more consecutive times
- `?` Matches either once or not at all
- `{n}` Matches n consecutive times

So, for example, the regexp [a-zA-Z0-9]{3} would match any string of three consecutive alphanumeric characters.

## Text Editors

If, up to this point, you have been struggling with the command-line text editors like vi and ee, you will be happy to know that now that you have X Windows running, you don't have to anymore. KDE comes with a couple of text editors similar to Notepad in Windows, but with many more features. The two editors available are simply named Text Editor and Advanced Editor. They look almost identical. Figure 18.10 shows the

You will only see these messages the first time.

FIGURE 18.10
*The KDE advanced editor.*

![](img/ba0161b65b37e94cffc801ecbacaba5e_322_0.png)

The main difference between the Text Editor and the Advanced Editor is that the Advanced Editor has more flexible searching functionality, as well as the capability to insert comments and indent text. Both editors have the capability to spell-check what you write. The basic features of the editors behave very similarly to most Windows or Macintosh text editing applications you are probably familiar with, so we aren't going to cover them here. Advanced features, such as commenting and paragraph formatting, are beyond the scope of this book.

> If you want to use one of the KDE text editors to edit a system configuration file, be aware that you need to be logged in as the root user (either by
logging in directly as root, or by logging in as a regular user and using su to gain root capabilities) and have started X Windows as the root user. If you start X while logged in directly as root, you will need to have an .xinitrc file in root's home directory (/root) in order to make KDE the default desktop. You can simply copy the one out of your home directory into root's directory.

![](img/ba0161b65b37e94cffc801ecbacaba5e_323_0.png)

Now that we have brought up the subject of text editors, it would be a good time to mention some tips about cutting and pasting text in X. All the KDE applets, and many other applications as well, can cut and paste text as you are used to doing it in Windows. In other words, select the desired text, click Edit, Copy and then move to the application you want to paste the text to and click Edit, Paste. However, not all applications support this. In this case, you can copy text by selecting it while holding down the left mouse button. You can then paste it by clicking the middle mouse button. This works for pasting text into terminal windows, in which you are running a command-line session, for example.

## File Management in KDE

The KDE file manager looks and behaves very much like the Windows Explorer. To access the file manager, click on the Home folder on your desktop. This will bring up the file manager displaying the contents of your home directory (see Figure 18.11).

FIGURE 18.11
The KDE file manager displaying a home directory.

![](img/ba0161b65b37e94cffc801ecbacaba5e_323_1.png)

## Moving and Copying Files and Folders

To move or copy a file or folder in the KDE file manager, move the mouse pointer over the file or folder you want to move or copy. Hold down the left mouse button and drag it to the location you would like to put it. When you release the mouse button, a menu will pop up asking what you want to do with the file. The options are Move, Copy, and Link. The first two options don't need any explaining; however, the third one might need a little bit. Basically, a Link is a pointer to the actual file. It allows you to access the file from somewhere other than where it is located without actually making a copy of it. You can think of a link as being the same thing as a shortcut in Windows.

If you change your mind and decide that you don't want to do anything with the file, simply click anywhere that is not on the pop-up menu and the operation will be canceled.

You can also move or copy a file or folder by right-clicking on it and then clicking Cut or Copy in the pop-up menu. You can then navigate to where you want to move or copy the file, right-click on a blank area of the file manager, and click Paste.

## Deleting Files or Folders

You can delete files or folders in the KDE file manager in four ways. The first is by dragging them to the trash can on the desktop. In this case, as in Windows and Macintosh, they are not really gone until you have emptied the trash. You can empty the trash by right-clicking on the trash can and clicking Empty Trash Bin.

The other three ways that you can delete a file or folder are by right-clicking on the file or folder and then selecting one of the menu options. The three menu options that allow you to delete a file or folder are as follows:

- **Move to Trash.** This option has the same effect as dragging the file to the trash can. Once again, the file is not really gone until you have emptied the trash.
- **Delete.** This option simply deletes the file. It is not moved to the trash bin. In other words, as soon as you have deleted the file, it is gone for good; so make sure that you really want to get rid of the file before selecting this option.
- **Shred.** This option deletes the file, and then writes over the area on the disk where the file was located several times. This basically ensures that the file is extremely difficult to recover—even with special software designed to recover deleted files.

## Changing File Attributes

To change the attributes of a file, right-click on it and then select Properties from the pop-up menu. In the box that pops up, click on the Permissions tab, which will bring up a dialog box like the one in Figure 18.12.
