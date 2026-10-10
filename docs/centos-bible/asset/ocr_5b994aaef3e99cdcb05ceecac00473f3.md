# ## GUI Doesn't Work at Startup

If CentOS has successfully installed (along with the desired desktop environment) but the GUI wasn't set to start at boot time, you may see only a simple text-based login prompt when you start CentOS. This login prompt may look something like this:

```
```text
CentOS release 5.2 (Final)
Kernel 2.6.18-92.1.22.el5 on an i686

localhost login:
```
```

Log in as the *root* user. As noted earlier, you can check if you have a GUI that is at least working well enough for you to correct it. Type the following command:

```
```bash
# startx
```
```

# ## What Happens during Desktop Startup?

The X server and graphical login screen is started by the `prefdm` script. By default, the login screen is displayed by the GNOME display manager (`gdm` command), which handles both logging in and starting the desktop environment for your console monitor, as well as graphical logins from other computers and X terminals.

The `prefdm` script is launched only if the run level in the `/etc/inittab` file is set to 5, as follows:

```
```text
id:5:initdefault:
```
```

If the `initdefault` state is 3, the system boots to a text-based login prompt. See Chapter 11 for information on Linux run states and start-up processes.

Some processes started during every X session are launched from scripts in the `/etc/X11/xinit/xinitrc.d` directory. Check those scripts to see if any of the settings they include might be causing problems. (You can also use those scripts to launch applications of your own each time X starts.)

If you are unable to get the video card and monitor configured properly or if you don't need a GUI, you can configure the computer to start up in text mode. To do this using any shell text editor (such as the `vi` command described in Chapter 4), change the `initdefault` line in the `/etc/inittab` file from `id:3:initdefault:` to `id:3:initdefault:`.

If you prefer to have CentOS boot to a GUI, change the 3 to a 5.

If the desktop works fine when you type **startx**, you might want to change to a graphical login, so the GUI starts automatically every time. See the "What Happens during Desktop Startup" sidebar for information on booting to a GUI. If X crashes, see `/var/log/Xorg.0.log` for clues about what went wrong.

If your GUI is so distorted you can't even see it to correct it, switch to a virtual terminal to correct the problem. For example, hold the [Ctrl] and [Alt] keys, and press [F2]. You will see a plaintext login prompt. Log in as *root* user and type **3** to make the garbled GUI login