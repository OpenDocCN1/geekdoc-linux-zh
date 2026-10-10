
```
POSITION_HINTS  5
ICON    logoicon.bm
LABEL   Instant Info
PUSH_ACTION    instinfo
}
```

4. Now be careful: this part is tricky. The next items have to have their POSITION_HINTS renumbered. But we are going to renumber only the next eight items, beginning with Mail and ending with Trash. Instead of 5 through 12, these are going to become 6 through 13.

5. Save the file.

Now, let’s restart the Workspace Manager. If we did everything right, we’ll have a new icon, which, when clicked, will bring up Instant Information, shown in Figure 14-9.

6. Position the mouse over a blank area on the workspace and press the right mouse button. Select Restart Workspace Manager.

![](img/eff8b9287a5f38c5adf538f24aacf29e_955_0.png)

Figure 14-9  Workspace Menu and New Subpanel and Action

A couple of things to remember when creating actions: first and foremost, make sure that the PUSH_ACTION and the file names are the same. That similarity is how they find each other. Make sure the that action file ends with .dt and make sure that the description file is executable. If any of these are wrong, the action either won't work or won't appear.

To avoid a lot of typing, sometimes the easiest approach is just to copy an existing definition and insert it where you want your new control to be and then modify it. As you move down the list of control definitions, you're moving from left to right across the front panel (notice that the POSITION_HINTS value increases in each definition). So if you want your new control to be to the right of the date on the front panel, you insert the control on the line below “date” and add a POSITION_HINTS 3 line to your definition; if you wanted your new control to be to the left of “date,” insert the control on the line above “date” with a `POSITION_HINTS` of 1.

The new control definition can be located anywhere in the list of control definitions. The `POSITION_HINTS` line keeps it from getting inadvertently bumped to a new position. It’s still a good idea to copy an existing definition and avoid extra typing; it reduces the chance of typing mistakes. And don’t forget to include the curly braces.

### Using Different Fonts

Although CDE fonts have been carefully selected for readability, you may have valid reasons to prefer other fonts. To make your fonts available system-wide throughout the CDE environment, put them in `/etc/dt/app-defaults/Dstyle` so that they will appear in the style manager’s font dialog box. To make fonts available only for a particular X client application, specify the font in the `app-defaults` file for the application. Just remember, this overrides the fonts in the style manager.

The font dialog box can contain a maximum of seven font sizes. You can adjust this number downward by resetting the value of `Dstyle*NumFonts` in `/etc/dt/app-defaults/Dstyle`; however, you can’t increase the number higher than seven.

The Font Dialog section of the `Dstyle` configuration file has seven `SystemFont` resources and seven `UserFont` resources. Again, you can have fewer than seven system and seven user fonts, but you can’t have more.

To specify fonts for a particular application, use the `*FontList` resource in the `app-defaults` file for the application.

To modify font resources on an individual user basis, you can use the `EditResources` action as described in the earlier section “Changing the Front Panel in Other Ways.”

### Changing the Login Messages

One of the nice things about CDE is the ability to modify so many parts. You can customize individual login accounts or the entire system. By customizing the login screen, you can show those about to log in the name of the system they are accessing, the company logo, and a personalized greeting. These modifications take place in the `Xresources` file:

1. As we’ve done already with the `dtwm.fp` and `dtwmrc` files, we will need to copy the system file from `/usr/dt/config/C` to `/etc/dt/config/C` as follows:

   `cp /usr/dt/config/C/Xresources /etc/dt/config/C/Xresources`

2. Go into your favorite editor and bring up the Xresources file so that it can be edited.

3. Go to the GREETING area. Here we’ll find the following lines:

   `!!Dtlogin*greeting.labelString:    Welcome to %LocalHost%`
   `!!Dtlogin*greetingpersLabelString:  Welcome %s`

   The first line is the message on the initial login screen. Let’s change that so that it welcomes us to our company, ABC, Inc.:

   1. Remove the comment notations. Unlike shell scripts that most of us are used to, the Xresources file uses two exclamation points as comment notation. Remove the `!!`.
   2. Next, modify “`Welcome to %LocalHost%`”. The `%LocalHost%` variable is replaced with our system name in the login screen. The line should look like this:

      `Dtlogin*greeting.labelString:    ABC, Inc. Welcomes You to %LocalHost%`

   3. Next let’s change the second line to include the department that this system is dedicated to: finance. This second line shows what is displayed when we are prompted for our password. The `%s` variable is our user name. The line should now look like this:

      `Dtlogin*greetingpersLabelString:    The Finance Department Welcomes %s`

   4. Save the file.

4. Now log out and back in. We should see the changes in the login screen. We didn’t need to “reload” the file, because the act of logging out and back in does that action.

## Changing the Login Picture

Adding a new picture to the login screen is easy if you know one thing. The file has to be a bitmap (.bm) or pixmap (.pm) file. A bitmap file is black and white, and the pixmap file is color. I’ve tried using other kinds of pictures (.gif and .jpg formats), but they just don’t display. The good news is that these can be imported from other systems or the Internet for our use. To make things simple, we’re going to use one already on the system. A bitmap showing a birthday cake was found in /usr/lib/X11/bitmaps on an HP-UX workstation. However, I have also successfully pulled down pictures of flowers, the Grand Canyon, and country music singers (note: Donna wrote this chapter, not Marty) from the Internet and put them on my system login screen.

1. Once more, let’s go into our favorite editor and modify `/etc/dt/config/C/Xresources`.

2. Go to the MISC area. Here we’ll find the following lines:
   ```
   !!Dtlogin*logo*bitmapFile:      < bitmap or pixmap file >
   ```

3. Delete the leading !!, which are the comment designators.

4. Replace < bitmap or pixmap file > with the name of the bitmap file using the entire path location. The line should look as follows:
   ```
   Dtlogin*logo*bitmapFile:       /usr/lib/X11/bitmap/cake.bm
   ```

5. Save the file.

6. Now log out and back in. We should see the birthday cake in the login screen. Again, we didn’t need to “reload” the file, because the act of logging out and back in does that task.

Now that we’ve seen how easily we can make some simple customizations in CDE for our end-users, we should be able to take this knowledge and really make their CDE environments a productive and friendly place to work.

# CDE - Advanced Topics

The Relationship among X, Motif, and CDE

X, OSF/Motif, and CDE are enabling framework technologies. Taken together, X, Motif, and CDE make up the three graphical layers on top of the operating system and hardware platform.

The GUI layers provide increasingly richer ease-of-use functions in a progressive series of layers that buffer the end user from the “user-hostile,” character-based interface of the operating system layer.

## The X Window System

The X Window System consists of the following:

- **Xlib** - Low-level library for programming window manipulation; graphics capabilities such as line drawing and text placement; controlling display output, mouse, and keyboard input; and application network transparency.
- **X11 Intrinsics** - Higher-level library for programming widgets and gadgets (graphical controls components like menus, scrollbars, and push buttons).
- **Display servers** - Hardware-specific programs, one per display, that manage the graphical input and output.
- **Interclient communication conventions (ICCC)** - A manual specifying standards for how X client programs should communicate with each other.
- **Configuration files** - One configuration file that specifies the default session to start (``sys.x11start``) and another specifying values for resources used to shape the X environment (``sys.Xdefaults``).

Through these mechanisms, X provides the standard upon which the graphical part of the network-oriented, client/server, distributed computing paradigm is based. A knowledge of **Xlib** and the **X11 Intrinsics** is important for programming in X and for programming at the Motif level. For system administrators, however, as long as the display servers work and X client applications are ICC-compliant, you shouldn’t need to delve into the X layer. CDE enables you to view X pretty much as part of “all that underlying
