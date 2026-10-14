passwd(1)      User Commands      passwd(1)
NAME
    passwd - change login password and attributes
SYNOPSIS
    passwd [ name ]
    passwd [ -d | -l ] [ -f ] [ -n min ] [ -w warn ]
          [ -x max ] name
    passwd -s [ -a ]
    passwd -s [ name ]

DESCRIPTION
    The passwd command changes the password or lists
    attributes associated with the user's login name.
--More--(5%)

(The man command pauses after each screenful and waits for you to press the spacebar before continuing.) The word More at the bottom of each page indicates how much of the help has so far been displayed. The terms in square brackets are optional parameters (-d, -l, -f, for example); vertical bars indicate that the terms on either side are mutually exclusive—you can use only one at a time.

For more information on getting help with Linux commands, see the section at the end of Chapter 4, "Living in a Shell," that discusses the GNOME Help Browser. The Help Browser operates in the X Windows environment and offers point-and-click access to several sources of help information.

# Use passwd to Change Your Password

You can use the passwd command to change your log-in password, and as you can tell from the man output shown in the preceding section, you have quite a few options. Here are some of the most common:

+   passwd          Change your own password
+   passwd sleepy   Change sleepy's password
+   passwd -d sleepy Delete sleepy's password

When you enter one of these commands to change a password, you will be prompted for the old (current) password and a new password. Your new password should be at least six characters long and not too easy for someone else to guess. Oh, and writing it down on a scrap of paper taped to your monitor is not recommended either. :-)