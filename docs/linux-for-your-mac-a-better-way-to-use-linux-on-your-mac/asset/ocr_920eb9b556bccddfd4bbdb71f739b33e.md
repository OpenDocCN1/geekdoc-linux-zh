![](bbox=[0.16, 0.07, 0.78, 0.34])

*Figure 9.17* Read a message by highlighting its subject and pressing *Enter*.

To read a message, press the *Enter* key and the message contents will be displayed on your screen. The *pine* command also features built-in help, and a spell-checker (using the default system spelling checker, usually the `ispell` or `aspell` command).

# Using mutt

The *mutt* command is a text-based electronic mail client similar to *pine*. This command also uses a resource file in your home directory named `.muttrc`. Like *pine*, it can also use a different resource file, like this:

```
$ mutt -F .mymuttrc
```

This mail client, shown in Figure 9.18, has a similar interface to *pine*, but a different set of top-level commands, such as:

+   * `\<BackSpace\>` Go to previous page
+   * `\<Space\>` Go to next page
+   * `?` Display help screen
+   * `d` Delete message
+   * `i` Exit *mutt*
+   * `j` Go to next message
+   * `x` Reply to message
+   * `v` View message attachment