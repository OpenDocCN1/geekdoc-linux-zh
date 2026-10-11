The next thing you need to do is tell the X font service (xfs) that the fonts are there and should be made available to remote X server clients. This is done by editing the /etc/X11/fs/config file, a sample of which follows:

```
fs2:/etc/X11/fs $ cat ./config
no-listen = tcp
port = 7100
client-limit = 10
clone-self = on
use-syslog = on
deferglyphs = 16
catalogue = /usr/share/fonts/misc:unscaled,
    /usr/share/fonts/75dpi:unscaled,
    /usr/share/fonts/100dpi:unscaled,
    /usr/share/fonts/japanese:unscaled,
    /usr/share/fonts/baekmuk:unscaled,
    /usr/share/fonts/Type1,
    /usr/share/fonts/URW,
    /usr/share/fonts/Speedo,
    /usr/share/fonts/CID,
    /usr/share/fonts/PEX,
    /usr/share/fonts/cyrillic,
    /usr/share/fonts/latin2/misc,
    /usr/share/fonts/latin2/75dpi,
    /usr/share/fonts/latin2/100dpi,
    /usr/share/fonts/latin2/Type1,
    /usr/share/fonts/latin7/75dpi,
    /usr/share/fonts/kwintv,
    /usr/share/fonts/truetype,
    /usr/share/fonts/uni,
    /usr/share/fonts/ucs/misc,
    /usr/share/fonts/ucs/75dpi,
    /usr/share/fonts/ucs/100dpi,
    /usr/share/fonts/hellas/misc,
    /usr/share/fonts/hellas/75dpi,
    /usr/share/fonts/hellas/100dpi,
    /usr/share/fonts/hellas/Type1
# in decipoints
default-point-size = 120
default-resolutions = 75,75,100,100
# font cache control, specified in KB
cache-hi-mark = 2048
cache-low-mark = 1433
cache-balance = 70
fs2:/etc/X11/fs $
```

Locate the no-listen = tcp line and remark it out with a # sign. Then review the catalogue = section and verify that your fonts directory is listed. When finished, save your changes to the file and exit your text editor.

At this point, you need to start the X font server. This is done by switching to your init script directory and entering ./xfs start at the shell prompt (as root). If desired, use the insvsvr or chkconfig commands to configure the xfs daemon to start every time the system boots. Then restart your X server.