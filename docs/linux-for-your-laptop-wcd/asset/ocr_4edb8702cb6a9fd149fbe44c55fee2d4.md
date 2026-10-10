characters; for example, use the `echo` command to send the proper escape sequence and codes:

```
$ echo -e '\033[32m'
```

After you press Enter, the characters will be green. To reset your console to the default, use this:

```
$ echo -e '\033[0m'
```

For other control codes, see the `console_codes` man page.

# ## Using Virtual Consoles

When you boot Linux to the command line, you see a login prompt. After you type your username and password, you're at the shell prompt. Yet another amazing feature of Linux is that you can then jump to another login prompt and log in again or log in as another user! In fact, most Linux distributions support at least six logins, or *virtual consoles*. (They support even more if you consider that you can run at least two additional X sessions at once. See the later section “Using Multiple X Sessions.”)

If you start at the Linux console, jumping to another console is quite easy. If you're using Intel-based Red Hat Linux, press Alt+F2. You'll then see another login prompt. If you're using Yellow Dog Linux on the iBook, press Ctrl+Cmnd+2, and you'll jump to another login prompt. On the iBook, press Ctrl+Cmnd+1 to jump back to the original login.

If you boot Linux directly to X11, you can jump to a console login screen by pressing Ctrl+Alt+F2. To jump back to your X11 session, press Alt+F7.

# Must Kill X11 on the iBook?

At the time this chapter was written, it appeared that if you use Yellow Dog Linux on the Apple iBook, there is no way to jump to a text-based console without pressing Ctrl+Opt+Cmnd+Del to kill the current X server. However, you can then jump between text logins at consoles 2-6 with ease by using Ctrl+Cmnd+1 (or 2-6 as appropriate).

Using multiple logins is a handy way to run different text-based applications at once in full-screen mode on your notebook. However, if you have only one screen available, such as if you have logged in remotely via a modem, you can use features available in some shells to temporarily suspend, and then retrieve, a running application.