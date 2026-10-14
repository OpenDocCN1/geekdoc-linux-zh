
## Control

Having described the controls to which this device will respond, it is then possible for remote controlling applications to send messages to the device. These are wrapped with the Simple Object Access Protocol (SOAP), meaning that you’ll be looking at a lot of XML!

## Event Notify

With the control layer being used to receive incoming messages, it only makes sense that the event notify layer is able to send them. This happens when a state on the device changes. The specifics of these events vary according to device, so when a “control point” first subscribes to the device, a list (again, in XML) is sent back, which details the events to which the control point can listen. It then makes a request to subscribe to these events, and so initiates a push mechanism between device and controller.

## Presentation

Ultimately, there is a layer whereby two devices have agreed that the media at a specific URL wants to be played, and that it should be played on a specific device. No indication is given in the specification on which media formats should be supported by the presentation layer, and therefore which files are compatible. This is “by design,” and it is something that the Digital Living Network Alliance has tackled. (For more on this, see later in this book.)

Because the presentation layer is separate from the control and server, the architecture provides us with one very sneaky built-in advantage! That is, it is easy to stream one signal to two different presentation components. On the surface, this provides a basic “whole-house audio” system, or a means to watch the same program in the living room and continue watching it in the kitchen. Indeed, this is possible. But because the presentation components do not need to match in terms of functionality, this means you can have a UPnP-enabled TV in the lounge but only a set of suitable speakers in the kitchen. In this way you can continue to listen to the program without being distracted by the visuals—something that may be of benefit if you’re working in the kitchen.

## Authentication

This is the seventh layer in our six-layer stack. That is to say . . . there is no authentication! Although this exemplifies our decision to not open ports and to our use of local network addresses, it does introduce a problem. In this case, the problem is not a technical one but a management one. If anyone on your local network can access your media, can you trust the people on your network? For the most part, these are members of your family who (should) conform to the social norms and coercions necessary to stop them abusing such access. However, you do only have a large-grain control mechanism, that is, removing their network access entirely, should this fail.

There are extensions to UPnP (such as the Device Security Service, and UPnP-UP (User Profile)) and protocols that are still not widely supported.

If you need authentication, however, and you can’t be sure that your younger children won’t take an interest in your certificate 15/18/X-rated films, then you might want to resort to Samba with password-protected areas for your media distribution. It is less well supported, and less flexible, than UPnP, but it would provide peace of mind.

## High-Level Separation of UPnP

Given the stack-based arrangement of the internal protocols, it is no surprise that the end user is introduced to this concept too, as there is a separation of functionality for the various parts of the system. This split is very natural and is comprised of:

- **server**—to provide media to other devices on the network
- **controller**—to start/stop the media, on any given device
- **renderer**—to display the media, be it video, pictures, or audio streams

This separation means that you can have any (or all) of the layers of functionality implemented on any given device. If they live on a single device, you have a standard media player. When the server is separated, you have the typical media streaming setup with the NAS playing the role of a server, while the streamer is a combined controller and renderer. When they're all separate, you can control any device from anywhere, using any media. This extends further, so that you can start watching a program on one device (or renderer), use the controller, and send a command to a different renderer to continue watching.

It also means you need to install three pieces of software.

### Server

There are several options here and the choice is best determined by the size of the machine that will be running it.

#### Minidlna

For miniature needs, such as the Raspberry Pi, we have the aptly named minidlna. This is miniature in size and presence, but it provides the standard functionality of audio, video, subtitles, and pictures out of the box. The biggest drawback is its lack of transcoding but, for a Linux-based HA solution, where the media renderers are able to cope with almost any format, this is an unnecessary drain on CPU cycles.

It can be downloaded from http://sourceforge.net/projects/minidlna/ or, for those using ArchLinux, retrieved as a package at https://www.archlinux.org/packages/?name=minidlna. Most of the other distros have yet to include it, so you will generally need to compile it. You will always need to include the development versions of the AV libraries on which it depends:

- libavcodec
- libavformat
- libavutil
- libexif

Additionally, depending on the versions, you might need to amend metadata.c to handle a change in the AV header files. Specifically, you had to amend metadata.c around line 715 and explicitly add:

```c
#define AV_DICT_IGNORE_SUFFIX 2
```

so that it precedes the function definition:

```c
#define AV_DICT_IGNORE_SUFFIX 2

sqlite_int64
GetVideoMetadata(const char * path, char * name)
{
```

Configuring the server requires you to edit the basic configuration file, to indicate the port, the appropriate locations of your media files, and the log files. This file is **minidlna.conf** and should be amended to begin:

```conf
# port for HTTP (descriptions, SOAP, media transfer) traffic
port=8200

# set this to the directory you want scanned.
media_dir=A,/net/media/mp3
media_dir=/net/media/movies

# set this if you would like to specify the directory where you want MiniDLNA to store its log file
log_dir=/var/log
```

Multiple media_dir lines are perfectly acceptable, and the “A” designation ensures that only Audio files are included. This is handy because some newer albums include digital tracks and music videos alongside their audio counterparts.

From here you can start the server as a daemon from a user account with:

```bash
minidlna -f minidlna.conf
```

At this point, it will scan the specified media directories for all your files, although the server will begin before scanning has completed. Consequently, some media players will need to be refreshed (or, in the worst case, restarted) to pick up files as the scanning procedure continues. It will also install an inotify notifier into the kernel to automatically look for new files in the media directories, although any changes to the configuration file to introduce new media will require you to restart the daemon. There is a command to force such a refresh:

```bash
minidlna -R
```

Although success with this option has been widely variable.

If you intend to include minidlna (or any other UPnP server) in your startup scripts in /etc/init.d, then include it at the end of the sequence, to ensure that filesystem services such as RAID are fully started.

The cache of media files is stored, by default, in /tmp. If you wish this to be more permanent, for example, between reboots, then add a line to the configuration file to this effect:

```conf
db_dir=/var/cache/minidlna
```

Although there is no web administration tool, you can retrieve basic stats by pointing your web browser to port 8200, or install webmin. In reality, however, little administration is needed as it is intended to be operated headless, with a controller such as VLC.

#### Rygel

As a media server, Rygel (https://live.gnome.org/Rygel) builds on the conceptual functionality of minidlna by incorporating its main omission—transcoding. Naturally, this requires a machine with higher performance than minidlna, but the software still retains its focus on being used on a headless box.

Like minidlna, Rygel can be run by a local user and is configured by specifying the URLs of your media:

```conf
# In ~/.config/rygel.conf
uris=/net/media/movies,/net/media/mp3
```
