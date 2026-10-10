name under the `/usr/local/bin` directory. If `/usr/local/bin` is not in your `$PATH`, you can either edit your default `$PATH` setting or configure the software to install under a different directory. You are now set to start ripping audio CDs!

# ## Using the krabber Client

KDE's `krabber` client, by Adrian Schroeter, is an easy to use audio CD ripping and encoding front-end that is also network aware. This means that you can use `krabber` to automatically retrieve information about your audio CD and save converted tracks with the song's name in a directory with the name of the album. Start `krabber` from the command line of an X11 terminal window like, this:

```
```
# krabber &
```
```

When you first use `krabber` it will look for a number of external commands that can be used to rip CDs. Its main window is shown in Figure 13.16 (just before ripping begins).

Set the CPU priority in order to devote the majority of your system's CPU horsepower to the task of encoding files. Select an appropriate bitrate for the resulting music files (higher rates result in larger `.mp3` files), along with various audio filters. Ripping an audio CD then consists of four steps:

+   1.  Select audio tracks from the inserted audio CD. Press the first button and you will be asked for the tracks to convert. Click the Done button, and then `krabber` will attempt to query a remote Internet music database in order to label your tracks.

![](bbox=[0.13, 0.65, 0.87, 0.93])

**Figure 13.16** KDE's `krabber` can automate the conversion of audio CDs into `.mp3` files.