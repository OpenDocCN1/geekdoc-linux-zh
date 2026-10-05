
# Chapter 7: Using SuSE Linux for the First Time

unique identity also helps to keep the actions of one person from affecting the actions of another, because many people may be using the same computer at the same time.

For now, you will be logging in as *root*, in Linux terms is known as superuser. The *superuser* is a privileged account that enables a person to go anywhere and do anything on the system. Superusers can add disk drives, do backups, restore damaged files, and turn the system off and on. They can also damage the system if they make a mistake. Because superusers are all-powerful, their mistakes can be all-bad.

Before doing more in this chapter, you need to create another account for yourself that is unprivileged. In that way, when you make a mistake while becoming familiar with Linux — and who doesn't? — it will be limited to the power of your account. You may erase your own files and data but not some else's files or the system's files. Comforting, isn't it?

Before you create a safe, new account for yourself, though, you need to log in as *root*. For that, you need the superuser password that you typed during installation (refer to Chapter 5):

```
login: root
Password:
```

You won't see the password while you type it on the screen. The secrecy ensures that your coworkers, who may be watching over your shoulder, will not see the password and try to log in later as *root*. So much for trust in the workplace.

If you make a mistake typing the password (or while typing the word *root*), the system responds with

```
Login incorrect
```

and gives you another chance by redisplaying

```
login:
```

Type **root** and then type your password.

After you are logged on as *root*, the following appears on the screen:

```
root@localhost:~ #
```

with a # as the final character. The # at the end of the line indicates that you are a superuser with extraordinary powers, so be careful.

![](img/96a9ce6a13d8d15ed05f867f41574278_146_0.png)

# 120 Part II: Installing SuSE Linux

We strongly recommend that you do most of your experimentation with Linux as a nonprivileged user and switch to superuser only when you absolutely need to.

The time comes to create that safe, nonprivileged user account. If you have installed X Window System, you can use YaST, which is already installed on your system, to add a user account. If you want to learn how to create an account without using YaST, you can go to the “Creating a General Account without YaST” section.

# Using YaST to create a General Account from within the X Window System

You can accomplish basic system administration tasks in SuSE Linux with YaST. YaST is the tool you use to install SuSE Linux, and when installation is complete, it is the tool you use to administer your Linux system. The YaST main menu, shown in Figure 7-1, appears when you click the YaST icon on the panel at the bottom of your screen.

![](img/96a9ce6a13d8d15ed05f867f41574278_147_0.png)

| YaST - Yet another Setup Tool- |
| :--- |
| YaST Version 1.01 - (c) 1994-99 SuSE GmbH |
| Language: English |
| Media: CD-ROM, EIDE /dev/hdc |
| Root-Device: /dev/hd3 |
| General help for installation |
| Adjustments of installation |
| Choose/Install packages |
| Update system |
| System administration | Show file for installation media |
| Copyright |
| Exit YaST |

1. At the system prompt, type startx like so:
   `root@localhost:~ # startx`
2. Click the YaST button on the panel.
   YaST is the button with the yellow star. If you hold the cursor over each of the icons on the panel, a description of the icon appears. The YaST main menu appears, as shown in Figure 7-1.

# Chapter 7: Using SuSE Linux for the First Time 12

3. Press the down-arrow key on the keyboard to select the System Administration menu item.

The System Administration submenu appears, as shown in Figure 7-2.

![](img/96a9ce6a13d8d15ed05f867f41574278_148_0.png)

Figure 7-2:
The System Administration submenu.

4. Press the down-arrow key on your keyboard to select the User Administration menu item.

The User Administration dialog box appears, as shown in Figure 7-3. This dialog box has a few fields that can be filled out. Fortunately, YaST does most of the work for you, as you will.

![](img/96a9ce6a13d8d15ed05f867f41574278_148_1.png)

Figure 7-3:
The User Administration dialog box.

# 122 Part II: Installing SuSE Linux

5. In the field labeled User Name, add the name of the account that you want to create.

After you add the username and press Enter, all the fields are automatically filled with the exception of the password field and the description field, as shown in Figure 7-4.

![](img/96a9ce6a13d8d15ed05f867f41574278_149_0.png)

| YAST | |
| :--- | :--- |
| User name | |
| User ID | |
| Group | |
| Home directory | |
| Shell | |
| Password | |
| Description | |

6. In the Description field on the bottom, fill in:
   - Make the username short (no more than eight characters) and lowercase.
   - Make the password difficult to guess, use a combination of uppercase, lowercase, and special characters. Do not use common words or nicknames.
   - Among the choices, use numbers if needed.

7. When the information is complete, press F4 to save your changes. The user account has been created. To exit this dialog box, press F10.

# Chapter 7: Using SuSE Linux for the First Time 150

# Meaningful names

The name that you choose for your login is also the name you will use to send and receive-mail, so choose the name carefully. Names that seem cute now may not later. Nor should you choose a name that is too long, because you may have to type it several times a day. Our corporate standards stated that the login name had to be the person's last name. As I created my account, I knew that people would have little chance of spelling it correctly, so I created my account as TomC. Tom Chielewski became known as TomC throughout the group, the department, and the entire company of 130,000 people. When Tom left the company, his new company had the same policy as ours. Before his first day was over,

# Adding a Printer

If you are logged in as root, you might want to take a few minutes to configure your printer. You can find a list of supported printers in Appendix A.

1. Start YaST as described in the previous section and select the System Administration submenu.
2. Integrate hardware into system from the menu list.
3. Select Configure Printers from the menu list.

You should now be looking at the printer configuration dialog box, shown in 7-5.

4. If you have a color printer, press the space; when an X appears in the box, press Enter.
5. Next you need to select the Printer Type. You have three options:
   * Postscript Printer: Select this option if you have a Postscript printer. When you press Enter, you are prompted to specify the resolution of your printer.
   * HP Deskjet: Select this option if you have a Hewlett Packard printer. When you press Enter, you are presented with a list of HP printers. Select your printer from the list. If your printer does not appear on the list, select the one that is closest to your printer. If you cannot find one, have a look in Appendix A, which contains a list of the available printer drivers and the different printers that support them.
