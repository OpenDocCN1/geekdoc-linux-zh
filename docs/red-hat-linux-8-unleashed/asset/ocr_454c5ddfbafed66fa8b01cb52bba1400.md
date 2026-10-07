If you don't use X, use Red Hat's kbdconfig command (as root) to change a keyboard type and language. This command can be used without an active X session (or if you are using X, from inside a terminal window) like this:

# # kbdconfig

After you press Enter, you'll see the Configure Keyboard dialog, as shown in Figure 4.1.

![](bbox=[0.343, 0.243, 0.656, 0.483])

FIGURE 4.1 The kbdconfig command can be used to choose a keyboard map (language) for Red Hat Linux.

This dialog enables you to choose a new keyboard type.

Scroll through the list to highlight a desired keyboard type, and then use the Tab key to highlight the OK button and press Enter. The listings represent entries under the /lib/kbd/keymaps/i386 directory, which are used to associate your keyboard's layout and keys with a language. The keyboard configuration is stored in the file /etc/sysconfig/keyboard, which might look like this:

```
KEYBOARDTYPE="pc"
KEYTABLE="us"
```

If you're using Red Hat during an X session, you can use the graphical interface to configure a keyboard language. To open the keyboard configuration dialog box, use the redhat-config-keyboard client at the command line of a terminal window, like so:

```
$ redhat-config-keyboard &
```

After you press Enter, you'll be prompted for the root password. Enter the password and click OK. You'll then see the Keyboard dialog box shown in Figure 4.2. This dialog box is similar to that displayed by kbdconfig.