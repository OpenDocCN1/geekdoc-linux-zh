| File Type | Filename Extension | MIME Type | Possible FreeBSD Helper Application |
|---|---|---|---|
| WAV audio files | .wav | audio/x-wav | /usr/local/bin/play |
| MP3 audio files | .mp3 | audio/mpeg | /usr/local/bin/x11amp |
| MPEEG video files | .mpg, .mpeeg, .mpe | video/mpeg | /usr/X11R6/bin/xanim |
| Quicktime video files | .mov, .qt | video/quicktime | /usr/X11R6/bin/xanim |
| AVI video files | .avi | video/x-msvideo | /usr/X11R6/bin/xanim |
| RealAudio files | .ra | audio/x-realaudio | /usr/local/bin/realplay |
| RealAudio files | .rpm | audio/x-pn-realaudio-plugin | /usr/local/bin/realplay |
| RealAudio files | .ram | audio/x-pn-realaudio | /usr/local/bin/realplay |
| RealVideo files | .rv | audio/vnd.rn-realaudio | /usr/local/bin/realplay |
| RealMedia files | .rm | video/vnd.rn-realvideo | /usr/local/bin/realplay |

> Table 27-1. Common AV File Types. Their Extensions and MIME Types, and Possible FreeBSD Players

Once you've linked the MIME type to an appropriate player, the next time you click on a link to that type of file, the web browser should launch the player application. It may first ask if you always want to link files of that type to your chosen application, though. If your viewer is a Linux viewer, you must enable Linux binary compatibility, as described in Chapter 4.

> In some cases, automatically launching the player is inadvisable—for example, when the file type can contain program code, such as a script or executable program. Also, some file formats may be mistaken for others; for instance, the .rpm extension used by RealPlayer files is also used by Red Hat Package Manager (RPM) package files for Linux programs. Web servers may therefore get the MIME type for such packages wrong.