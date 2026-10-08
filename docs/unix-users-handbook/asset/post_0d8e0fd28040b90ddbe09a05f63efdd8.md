
# Using Different Fonts

Although CDE fonts have been carefully selected for readability, you may have valid reasons to prefer other fonts. To make your fonts available system-wide throughout the CDE environment, put them in `/etc/dt/app-defaults/Dstyle` so that they will appear in the style manager’s font dialog box. To make fonts available only for a particular X client application, specify the font in the app-defaults file for the application. Just remember, this overrides the fonts in the style manager.

The font dialog box can contain a maximum of seven font sizes. You can adjust this number downward by resetting the value of `Dstyle*NumFonts` in `/etc/dt/app-defaults/Dstyle`; however, you can’t increase the number higher than seven.

The Font Dialog section of the **Dtstyle** configuration file has seven **SystemFont** resources and seven **UserFont** resources. Again, you can have fewer than seven system and seven user fonts, but you can't have more.

To specify fonts for a particular application, use the ***FontList*** resource in the **app-defaults** file for the application.

To modify font resources on an individual-user basis, you can use the **EditResources** action as described in the earlier section "Changing the Front Panel in Other Ways."

# Changing the Login Messages

One of the nice things about CDE is the ability to modify so many parts. You can customize individual login accounts or the entire system. By customizing the login screen, you can show those about to log in the name of the system they are accessing, the company logo, and a personalized greeting. These modifications take place in the **Xresources** file:

1. As we've done already with the **dtwm.fp** and **dtwmrc** files, we will need to copy the system file from `/usr/dt/config/C` to `/etc/dt/config/C`.
   ```bash
   cp /usr/dt/config/C/Xresources /etc/dt/config/C/Xresources
   ```

2. **Go into your favorite editor** and bring up the **Xresources** file so that it can be edited.

3. **Go to the GREETING area**. Here we'll find the following lines:
   ```text
   !!Dtlogin*greeting.labelString:		Welcome to %LocalHost%
   !!Dtlogin*greetingpersLabelString:	Welcome %s
   ```

The first line is the message on the initial login screen. Let’s change that so that it welcomes us to our company, ABC, Inc.:

1. **Remove the comment notations.** Unlike shell scripts that most of us are used to, the Xresources file uses two exclamation points as comment notation. Remove the `!!`.

2. Next, **modify “Welcome to %LocalHost%”**. The `%LocalHost%` variable is replaced with our system name in the login screen. The line should look like this:
   `Dtlogin*greeting.labelString: ABC, Inc. Welcomes You to %LocalHost%`

3. Next let’s **change the second line** to include the department that this system is dedicated to: finance. This second line shows what is displayed when we are prompted for our password. The `%s` variable is our user name. The line should now look like this:
   `Dtlogin*greetingpersLabelString: The Finance Department Welcomes %s`

4. **Save the file.**

5. Now **log out and back in**. We should see the changes in the login screen. We didn’t need to “reload” the file, because the act of logging out and back in does that action.

# Changing the Login Picture

Adding a new picture to the login screen is easy if you know one thing. The file has to be a bitmap (.bm) or pixmap (.pm) file. A bitmap file is black and white, and the pixmap file is color. I’ve tried using other kinds of pictures (.gif and .jpg formats), but they just don’t display. The good news is that these can be imported from other systems or the Internet for our use. To make things simple, we’re going to use one already on the system. A bitmap showing a birthday cake was found in `/usr/lib/X11/bitmaps` on an HP-UX workstation. However, I have also successfully pulled down pictures of flowers, the Grand
