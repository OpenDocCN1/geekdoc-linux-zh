# Starting Multiple X Sessions

You can also use startx to start multiple X11 sessions on the same computer, possibly using different window managers, and then navigate between the sessions using virtual consoles. SuSE Linux supports up to six different login screens or consoles, accessed by pressing Alt+X, where X is F1 through F6. For example, if you log in to Linux without using a display manager, you'll be at the first virtual console. After you log in, press Alt+F2; you'll then see another login prompt at the second console. Get back to your first login, press Alt+F1.

When you log in to SuSE Linux and start an X11 session with startx, X uses a seventh virtual screen. Because you've started X from the first virtual console, this console will be unavailable for use. However, you can get to another virtual console, as the second, by pressing Ctrl+Alt+F2. You'll then see the Linux login prompt. To go back to your X session, press Alt+Fkey7. Using this approach, you can jump back and forth between your X session and different text consoles.

To use multiple X sessions at different color depths on different virtual consoles, first start a session with the startx command. After the X desktop appears, press Ctrl+Alt+F2 and log in to Linux again. If your graphics card supports thousands of colors again, use the startx command to start an X session. This time, however, include the :1, -bpp 16, and vt8 command-line options:

```
# startx -- :1 -bpp 16 vt8
```

The screen clears and you'll be running an X session with a different color depth. To jump to your other session, press Ctrl+Alt+F7. To jump to another virtual console, press Ctrl+Alt+F3 (since the first and second consoles are in use). To jump back to your original X session, press Ctrl+Alt+F8.

# Starting Specific Window Managers

Under SuSE Linux, the startx command can be used to start a specific X11 window manager for an X11 session directly from the command-line interface of the console. You can also combine other startx options, such as color depth or display designations, to start multiple X11 sessions using different window managers at different color depths on the computer.

For example, you can start the AfterStep window manager for your initial X11 session:

```
# startx afterstep
```

![](bbox=[0.883, 0.617, 0.989, 0.778])