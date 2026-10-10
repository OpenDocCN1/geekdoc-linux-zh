# > NOTES

Do not use either the bare *pid* or *pid,start-ti* syntax forms for `—process`. There are race conditions in both. New code should always use *pid,pid-start-ti,uid*. The value of *start-ti* can be determined by consulting e.g. the (5) file system depending on the operating system. If fewer than 3 argunts are passed, **pkcheck** will attempt to look up them up internally, but note that this may be racy.

If your program is a daemon with e.g. a custom Unix domain socket, you should determine the *uid* parater via operating system chanisms such as PEERCRED.