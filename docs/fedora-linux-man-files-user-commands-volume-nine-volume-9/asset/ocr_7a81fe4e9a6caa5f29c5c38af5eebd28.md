# OPTIONS

-h

Print a short description of all command line options

-d

Log debug ssages

-s port

Set virtio serial *port* (default: /dev/virtio-ports/com.redhat.spice.0)

-x

Don’t daemonize

-f dir|xdg-desktop|xdg-download

Set directory where to save files send from the client, this can be either an arbitrary *dir* or one of the special values of *xdg-desktop* or *xdg-download* to select the default xdg Desktop resp. xdg Download directory. If no value is specified the default is *xdg-desktop* when running under a Desktop Environnt which has icons on the desktop and *xdg-download* under other Desktop Environnts

-o 0|1

Disable/enable opening the file save directory with xdg-open (showing the directory in the file manager) when a file transfer from the client completes. If no value is specified the default is *0* when running under a Desktop Environnt which has icons on the desktop and *1* under other Desktop Environnts