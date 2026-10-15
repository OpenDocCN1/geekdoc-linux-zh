![](bbox=[0.31, 0.115, 0.67, 0.36])

# FIGURE 22.7 Screen coordinate system.

A more complete listing of toolkit options and options for the xterm command is given in the man page on your system for xterm.

The following session shows how to run other applications using command line options. The three applications we run—xclock, xbibf, and xterm—are sized and positioned with the -geometry command line option and its arguments, which are the same for all three applications. Xclock displays an analog time-of-day clock on the screen as an icon. Xterm opens a CUI to the UNIX operating system. In order to size and position the application windows on your display screen, you must be aware of the way in which the screen coordinates are derived. The coordinate system for screen locations in the X Window System is shown in Figure 22.7.

Notice that the origin, 0 in X and 0 in Y, is in the upper-left corner of the screen, and the direction of increasing X is to the right and increasing Y is down. Of course the screen resolution of your display, in other words how many pixels in X and Y can be addressed, is dependent on what kind of monitor and graphics card you have available, and what your X Window System preferences are set to. To run the applications, in an xterm window type the following:

```
$ xclock -geometry 100x100+10+10 &
$ xterm -geometry 80x24+200+10 &
$
```

The upper-left corner of Figure 22.8 shows the appearance and relative size and position of each of the application windows after the previous two commands have been typed in. The arguments for the -geometry option are as follows: X-pixel size of window, Y-pixel size of window, X-position of upper-left corner of window, Y-position of upper-left corner of window. So the line xclock -geometry 100x100+10+10 sizes the xclock to be 100 by 100 pixels, and positions its upper-left corner at the coordinates X=10, Y=10 relative to 0,0.

To close down an X Window System application gracefully, you can use the client application mechanisms, which might be a pull-down menu choice or a button press. To close xclock or xbibf, you can find the PID of each by using the ps command, and then issue a kill signal for that PID. For example, if xclock had a PID of 904, as shown in the output from ps, then typing the following command in an xterm window would close the xclock application:

```
$ kill -9 904
```