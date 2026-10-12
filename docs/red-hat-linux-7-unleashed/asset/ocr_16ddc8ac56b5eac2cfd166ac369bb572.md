Half of the clients listed in Table 8.3 may be used from the command line of an X11 terminal window, or in the case of the xwd client, from the text-only console command line. The xwd client is used to take a snapshot of a running client or the root display of an X11 session. The output of the xwd command is sent directly to the standard output, so you’ll need to use file redirection or the -out command-line option, along with a filename to save your graphic.

For example, if you’re running X, you can press Ctrl+Alt+F2 to jump to the second virtual console, then use the xwd client to take a snapshot of your current X session like this:

```
# xwd -out shot1.xwd -root -display :0
```

# Note

> Note that you may have to enable access to your X11 session before taking screenshots from the console. You can do this by using the xhost command, followed by an allowed hostname (such as stinky.home.org), or a plus sign (+) to allow any host. Note that for security, afterwards you should rescind access by using the xhost and its minus option (-).

You can also use xwd from the command line of an X11 terminal window like this:

```
# xwd >out.xwd
```

After you press Enter, your cursor will turn into a cross-hair, and you can then click on another window or the root desktop to take a picture. To display your screenshot, you can use the xwd client like this:

```
# xwd <out.xwd
```

After you press Enter, the image will be displayed in a window. Click on the window to end the program.

# Taking Screenshots with the import Command

Another capable client you can use to take pictures of the root display or selected windows is the import command, part of John Crissy’s ImageMagick software package. This command, like xwd, is used from the command line, but features on-the-fly sizing, cropping, and rotation operations, along with graphics conversion. You can also use this command to take screenshots of other computers on your network (as long as you’re properly authorized, perhaps with the xhost command). And, like xwd, you can use the import command from the text-only console while an X11 session is running to take pictures of a root display.