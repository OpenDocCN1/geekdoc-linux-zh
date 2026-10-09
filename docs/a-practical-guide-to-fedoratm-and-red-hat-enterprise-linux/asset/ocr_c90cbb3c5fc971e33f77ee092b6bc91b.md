If you frequently work with other users via a network, you might find it convenient to add an `xhost` line to your `.bash_profile` file (page 330)—but see the tip on the previous page regarding security and `xhost`. Be selective in granting access to your X display using `xhost`; if another system has access to your display, you might find your work frequently interrupted.

# ## The DISPLAY Variable

The most common method of identifying a display is to use the `DISPLAY` shell environment variable to hold the X server ID string. This locally unique identification string holds the screen number of a display:

```
```bash
$ echo $DISPLAY
:0
```
```

The format of the complete (globally unique) ID string for a display is

**_[_host name_]:[display-number]:[screen-number]_**

where _host name_ is the name of the system running the X server, _display-number_ is the number of the logical (physical) display (0 unless multiple monitors or graphical terminals are attached to the system, or if you are running X over `ssh`), and _screen-number_ is the logical number of the (virtual) terminal (0 unless you are running multiple instances of X). When you are working with a single physical display, you can shorten the identification string. For example, you can use `plum:0.0` or `plum:0` to identify the only physical display on the system named `plum`. When the X server and the X clients are running on the same system, you can shorten this identification string even further to `0.0` or `:0`. An `ssh` connection shows `DISPLAY` as `localhost:10.0`. You might have to connect using `ssh` to see this value. See “X11 forwarding” on page 687 for information on setting up `ssh` so it forwards X.

# ### When you change the value of DISPLAY

When you change the value of the `DISPLAY` variable, all X programs send their output to the new display named by `DISPLAY`.

If `DISPLAY` is empty or not set, the screen you are working from is not running X. An application (the X client) uses the value of the `DISPLAY` variable to determine which display, keyboard, and mouse (collectively, the X server) to use. One way to run an X application, such as `gnome-calculator`, on the local system but have it use the X display on a remote system is to change the value of the `DISPLAY` variable on the client system so it identifies the remote X server.

```
```bash
sam@gua va:~$ export DISPLAY=lum:0.0
sam@gua va:~$ gnome-calculator &
```
```

The preceding example shows Sam running `gnome-calculator` with the default X server running on the system named `plum`. After setting the `DISPLAY` variable to the ID of the `plum` server, all X programs (clients) Sam starts use `plum` as their server (i.e., output appears on `plum`'s display and input comes from `plum`'s keyboard and mouse).